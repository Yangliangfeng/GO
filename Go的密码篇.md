## Go涉及的加密
### 存储密码
* md5, sha1, sha256

目前用的最多的密码存储方案是将明文密码做单向哈希后存储，单向哈希算法有一个特征：无法通过哈希后的摘要(digest)恢复原始数据，常用的单向哈希算法包括
SHA-256, SHA-1, MD5等。Go语言对这三种加密算法的实现如下所示：
```
1. sha256
h := sha256.New()
io.WriteString(h, "123456")
pwd := fmt.Sprintf("%x", string(h.Sum(nil)))

2. sha1
h := sha1.New()
io.WriteString(h, "123456")
pwd := fmt.Sprintf("%x", string(h.Sum(nil)))

3. md5
h := md5.New()
io.WriteString(h, "123456")
pwd := fmt.Sprintf("%x", string(h.Sum(nil)))
```
单向哈希有两个特性：
  * 1）同一个密码进行单向哈希，得到的总是唯一确定的摘要。
  * 2）计算速度快。随着技术进步，一秒钟能够完成数十亿次单向哈希计算。

结合上面两个特点，考虑到多数人所使用的密码为常见的组合，攻击者可以将所有密码的常见组合进行单向哈希，得到一个摘要组合, 然后与数据库中的摘要进行比对即可获得对应的密码。
这个摘要组合也被称为`rainbow table`。

* 加salt的md5, sha1, sha256

没有攻不破的盾，但也没有折不断的矛。现在安全性比较好的网站，都会用一种叫做“加盐”的方式来存储密码，也就是常说的 “salt”。他们通常的做法是，先将用户输入的密码进行一次MD5
（或其它哈希算法）加密；将得到的 MD5 值前后加上一些只有管理员自己知道的随机串，再进行一次MD5加密。这个随机串中可以包括某些固定的串，也可以包括用户名（用来保证每个用户加
密使用的密钥都不一样）。
```
h := md5.New()
io.WriteString(h, "123456")

//pwmd5等于e10adc3949ba59abbe56e057f20f883e
pwmd5 :=fmt.Sprintf("%x", string(h.Sum(nil)))

//指定两个 salt： salt1 = @#$%   salt2 = ^&*()
salt1 := "@#$%"
salt2 := "^&*()"

//salt1+用户名+salt2+MD5拼接
io.WriteString(h, salt1)
io.WriteString(h, "abc")
io.WriteString(h, salt2)
io.WriteString(h, pwmd5)

last :=fmt.Sprintf("%x", string(h.Sum(nil)))
```
* scrypt加密

只要时间与资源允许，没有破译不了的密码，所以，怎么解决这个问题呢？方案是:故意增加密码计算所需耗费的资源和时间，使得任何人都不可获得足够的资源建立所需的rainbow table。

这类方案有一个特点，算法中都有个因子，用于指明计算密码摘要所需要的资源和时间，也就是计算强度。计算强度越大，攻击者建立`rainbow table`越困难，以至于不可继续。

这里推荐scrypt方案，scrypt是由著名的FreeBSD黑客Colin Percival为他的备份服务Tarsnap开发的。

```
scrypt.Key([]byte("input your password"), salt, N, r, p, keyLen)
1. N is a CPU/memory cost parameter, which must be a power of two greater than 1. this is N = 32768
2. r and p must satisfy r * p < 2³⁰.
3. generate your own random salt. 8 bytes is a good length.
4. you can get a derived key for e.g. AES-256 (which needs a 32-byte key), as keyLen = 32

salt := []byte("abcdefgh")
dk, err := scrypt.Key([]byte("input your password"), salt, 32768, 8, 1, 32)
if err != nil {
    log.Fatal(err)
}
fmt.Println(base64.StdEncoding.EncodeToString(dk))
```
### 加密和解密数据
* base64加解密

如果Web应用足够简单，数据的安全性没有那么严格的要求，那么可以采用一种比较简单的加解密方法是base64，这种方式实现起来比较简单，如下:
```
func base64Encode(src []byte) []byte {
	return []byte(base64.StdEncoding.EncodeToString(src))
}

func base64Decode(src []byte) ([]byte, error) {
	return base64.StdEncoding.DecodeString(string(src))
}

func main() {
	// encode
	hello := "你好，世界！ hello world"
	debyte := base64Encode([]byte(hello))
	fmt.Println(debyte)
	// decode
	enbyte, err := base64Decode(debyte)
	if err != nil {
		fmt.Println(err.Error())
	}

	if hello != string(enbyte) {
		fmt.Println("hello is not equal to enbyte")
	}

	fmt.Println(string(enbyte))
}
```
* 高级加解密---AES加密算法

crypto/aes包：AES(Advanced Encryption Standard)，又称Rijndael加密法，是美国联邦政府采用的一种区块加密标准。
* Go代码实现
```
type AesEncrypt struct {
}
func (aes *AesEncrypt) getKey(key string) []byte {
    keyLen := len(key)
    if keyLen < 16 {
        painc("key of lenght not less than 16)
    }
    arrKey := []byte(key)
    if keyLen >= 32 {
        return arrKey[:32]
        //slice 32
    }
    if keyLen >= 24 {
        return arrKey[:24]
        //slice 24
    }
    return arrKey[:16]
}
//加密字符串
func (this *AesEncrypt) Encrypt(strMesg string) ([]byte, error) {
    key := this.getKey()
    var iv = []byte(key)[:aes.BlockSize]
    encrypted := make([]byte, len(strMesg))
    aesBlockEncrypter, err := aes.NewCipher(key)
    if err != nil {
        return nil, err
    }
    aesEncrypter := cipher.NewCFBEncrypter(aesBlockEncrypter, iv)
    aesEncrypter.XORKeyStream(encrypted, []byte(strMesg))
    return encrypted, nil
}
//解密字符串
func (this *AesEncrypt) Decrypt(src []byte) (strDesc string, err error) {
    defer func() {
        //错误处理
        if e := recover(); e != nil {
            err = e.(error)
        }
    }()
    key := this.getKey()
    var iv = []byte(key)[:aes.BlockSize]
    decrypted := make([]byte, len(src))
    var aesBlockDecrypter cipher.Block
    aesBlockDecrypter, err = aes.NewCipher([]byte(key))
    if err != nil {
        return "", err
    }
    aesDecrypter := cipher.NewCFBDecrypter(aesBlockDecrypter, iv)
    aesDecrypter.XORKeyStream(decrypted, src)
    return string(decrypted), nil
}
func main() {
    aesEnc := AesEncrypt{}
    arrEncrypt, err := aesEnc.Encrypt("abcde")
    if err != nil {
        fmt.Println(arrEncrypt)
        return
    }
    strMsg, err := aesEnc.Decrypt(arrEncrypt)
    if err != nil {
        fmt.Println(arrEncrypt)
        return
    }
    fmt.Println(strMsg)
}
```

  
