# 冒泡排序

```go
func bubbleSort(arr *[5]int) {
    for i := 0; i < len(*arr)-1; i++ {
        for j := 0; j < len(*arr)-1-i; j++ {
            temp := 0
            if (*arr)[j] > (*arr)[j+1] {
                temp = (*arr)[j]
                (*arr)[j] = (*arr)[j+1]
                (*arr)[j+1] = temp
            }
        }
    }
}
```
