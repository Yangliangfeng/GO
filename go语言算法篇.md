## 冒泡排序
* 冒泡排序原理
```
1. 从下标为 0 到 n-1 的元素.即（0，n-1）,依次比较相邻两个元素，把最大（或最小）的数移动到最右边位置，即下标为 n-1处
2. 再从下标为 0 到 n-2 的元素.即（0，n-2），依次比较相邻两个元素，把最大（或最小）的数移动到 最右边-1 位置，即下标
   为 n-2 处
3. 一直重复 n躺 即可达到排序效果
```
* Go的冒泡排序
```
func bubblesort(values []int) []int {
    ii := len(values)
    for i := 0; i < ii; i++ {
        for j := 0; j < ii - i - 1; j++ {
           if values[j] < values[j + 1] {
                values[j], values[j + 1] = values[j + 1], values[j]
           }
        }
    }
    return values
}
```
* 冒泡排序的时间复杂度
```
其复杂度为O(N^2)
```
* 冒泡排序的改进
```
给定一个整数序列{6,1,2,3,4},每完成一次外层循环的结果为：
6,1,2,3,4
1,2,3,4,6 此时 i = 0；
1,2,3,4,6 此时 i = 1；
1,2,3,4,6 此时 i = 2；
1,2,3,4,6 此时 i = 3；
我们发现第一次外层循环之后就排序成功了，但是还是会继续循环下去，造成了不必要的时间复杂度
```
* Go改进后的冒泡排序
```
func bubblesort(values []int) []int {
    var flag bool
    ii := len(values)
    for i := 0; i < ii; i++ {
        flag = true
        for j := 0; j < ii - i -1; j++ {
            if  values[j] < values[j + 1] {
                values[j], values[j + 1] = values[j + 1], values[j]
                flag = false
            }
        }
        if flag == true {
            break
        }
    }
    return values
}
```
