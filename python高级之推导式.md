## 推导式（Comprehensions）
如果你已经使用了很长时间的Python，那么你至少应该听说过列表推导(list comprehensions)。
这是一种将for循环、if表达式以及赋值语句放到单一语句中的一种方法。换句话说，你能够通过一个表达式对一个列表做映射或过滤操作。

一个列表推导式包含以下几个部分：

1. 一个输入序列  
1. 一个表示输入序列成员的变量  
1. 一个可选的断言表达式
1. 一个将输入序列中满足断言表达式的成员变换成输出列表成员的输出表达式  

举个例子，我们需要从一个输入列表中将所有大于0的整数平方生成一个新的序列，你也许会这么写：  

	num = [1,4,-5,10,-7,2,3,-1]
	filtered_and_squared = []
	
	for number in num:
		if number > 0:
			filtered_and_squared.append(number ** 2)
	print(filtered_and_squared)
	# [1,16,100,4,9]
	
很简单是吧？但是这就会有4行代码，两层嵌套外加一个完全不必要的append操作。
而如果使用filter、lambda和map函数，则能够将代码大大简化：

	num = [1,4,-5,10,-7,2,3,-1]
	filtered_and_squared = map(lambda x: x ** 2, filter(lambda x: x>0, num))
	print(filtered_and_squared)
	# [1,16,100,4,9]
	
嗯，这么一来代码就会在水平方向上展开。
那么是否能够继续简化代码呢？列表推导能够给我们答案：

	num = [1,4,-5,10,-7,2,3,-1]
	filtered_and_squared = [x**2 for x in num if x &gt; 0]
	print(filtered_and_squared)
	# [1,16,100,4,9]
	
![列表推导式图解](http://jbcdn2.b0.upaiyun.com/2014/02/8db6c2a8d716d7788d0e526c921cc504.jpg)

* 迭代器（iterator）遍历输入序列num的每个成员x  
* 断言式判断每个成员是否大于零  
* 如果成员大于零，则被交给输出表达式，平方之后成为输出列表的成员  

列表推导式被封装在一个列表中，所以很明显它能够立即生成一个新列表。
这里只有一个type函数调用而没有隐式调用lambda函数，列表推导式正是使用了一个常规的迭代器、一个表达式和一个if表达式来控制可选的参数。  

另一方面，列表推导也可能会有一些负面效应，那就是整个列表必须一次性加载与内存之中，
这对上面举的例子而言不是问题，甚至扩大若干倍之后也都不是问题。但是总会达到极限，内存总会被用完。  

针对上面的问题，生成器（Generator）能够很好的解决。生成器表达式不会依稀将整个列表加载到内存之中，
而是生成一个生成器对象（Generator objector），所以一次只加载一个列表元素。  

生成器表达式同列表推导式有着几乎相同的语法结构，区别在于生成器表达式是被圆括号包围，而不是方括号：  

	num = [1,4,-5,10,-7,2,3,-1]
	filtered_and_squared = (x**2 for x in num if x > 0)
	print(filtered_and_squared)
	
	# <generator object <genexpr> at 0x00583E18>
	
	for item in filtered_and_squared:
		print(item)
		
	# 1, 16, 100, 4, 9
	
这比列表推导效率稍微提高一些，让我们再一次改造一下代码：  

	num = [1,4,-5,10,-7,2,3,-1]
	
	def square_generator(optional_parameter):
		return (x**2 for x in num if x > optional_parameter)
		
	print square_generator(0)
	# <generator object <genexpr> at 0x004E6418>
	
	# Option
	for k in square_generator(0):
		print(k)
	# 1, 16, 100, 4, 9
	
	# Option 2
	g = list(square_generator(0))
	print(g)
	# [1,16,100,4,9]
	
除非特殊的原因，应该经常在代码中使用生成器表达式。
但除非是面对非常大的列表，否则是不会看出明显区别的。  

下例使用zip()函数一次处理两个或多个列表中的元素：  

	alist = ['a1', 'a2', 'a3']
	blist = ['1', '2', '3']
	
	for a, b in zip(alist, blist):
		print(a,b)
		
	# a1 1
	# a2 2
	# a3 3
	
再来看一个通过zip()函数得到对应的字典：  

	list1 = ['a', 'b', 'c']
	list2 = [1, 2, 3]
	dict_out_put = dict(zip(list1, list2))
	print(dict_out_put)
	
	# {'a':1, 'b':2, 'c':3}
	
