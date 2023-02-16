---
created: 2023-01-17
type: Literature Note
tag: TODO
url: 
share: true
---
>[!success] 要点
>- 一般是用递归实现
>- 

## 1. 算法步骤
![[分治算法（Divide-and-conquer algorithm）.png | center | 600]] <i class="figcaption" id="center">分治算法示意图[^2]</i>

A typical Divide and Conquer algorithm solves a problem using following three steps.

1.  **Divide**: Break the given problem into sub-problems of same type.
2.  **Conquer**: Recursively solve these sub-problems
3.  **Combine**: Appropriately combine the answers

其中 Divide 步骤和原问题只有数据规模上的差异，一般来说分治算法都是用递归实现，有如下代码架构
```python
def function(data):

	# 1.递归终止条件
	if data==BC:
		return value
		
	# 2.分解成子问题
	sub_return1 = function(sub_data1)
	sub_return2 = function(sub_data2)
	...

	# 3.将子问题合并
	return combine(sub_return1,sub_return2,...)
	
```
所以只需要考虑以下三个问题：
- 怎么分解为子问题（一般减少数据规模）
- 递归终止条件是什么
- 怎么将子问题合并（关键代码）

## 2.

>[!note] 与[[递归（Recursion）]]的区别
>- Recursion is a "==Programming Paradigm==" which is *generally* used to implement the "Algorithmic Paradigm" Divide and Conquer .[^1]
>- 不是所有的递归都是分治算法，递归也可以用于其他类型算法，比如 [[decrease-and-conquer]][^3]





## 参考文献

[^1]: https://qr.ae/prAVXW
[^2]: https://www.enjoyalgorithms.com/blog/divide-and-conquer
[^3]: https://www.geeksforgeeks.org/decrease-and-conquer/