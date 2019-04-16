## 序列
- 首先需要有序列的概念, list只是序列的一种

## bisect用于维护已排序序列
- 使用bisect插入数据会将数据按顺序排序(升序)
- bisect利用二分查找来维护排序序列

```
import bisect

inter_list = []
bisect.insort(inter_list, 3)
bisect.insort(inter_list, 2)
bisect.insort(inter_list, 5)
bisect.insort(inter_list, 1)
bisect.insort(inter_list, 6)
print(inter_list)
>>> [1, 2, 3, 5, 6]

print(bisect.insort_left(inter_list, 4))
>>> None
print(inter_list)
>>> [1, 2, 3, 4, 5, 6]
print(bisect.insort_left(inter_list, 3.0))
print(inter_list)
[1, 2, 3.0, 3, 4, 5, 6]
```
其中默认插入是右边插入`insort = insort_right`

- 查找将会插入的位置
```
inter_list = [1, 2, 3.0, 3, 4, 5, 6]
print(bisect.bisect(inter_list,2.0))
>>> 2
```
其中默认插入是右边插入`bisect = bisect_right`