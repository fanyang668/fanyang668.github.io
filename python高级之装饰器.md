## 装饰器（Decorators）
装饰器为我们提供了一个增加已有函数或类的功能的有效方法。听起来是不是很像Java中的面向切面编程（Aspect-Oriented Programming）概念？
两着都很简单，并且装饰器有着更为强大的功能。举个例子，假定你希望在一个函数的入口和退出点做一些特别的操作（比如一些安全、追踪以及锁定等操作）就可以使用装饰器。  

装饰器是一个包装了另一个函数的特殊函数：主函数被调用，并且返回值将会被传给装饰器，接下来装饰器将返回一个包装了主函数的替代函数，程序的其他部分看到的将是这个包装函数。  

	def time_this(func):
		'''Decorator that reports the execution time.'''
		pass
		
	@time_this
	def count_down(n):
		while n > 0:
			n -= 1
			
语法糖@标识了装饰器。  

好了，让我们回到刚才的例子。我们将用装饰器做一些更典型的操作：  

	import time
	from functools import wraps
	
	def time_this(func):
		'''Decorator that reports the execution time.'''
		@wraps(func)
		def wrapper(*args, **kwargs):
			start = time.time()
			result = func(*args, **kwargs)
			end = time.time()
			print(func.__name__, end-start)
			return result
		return wrapper 
		
	@time_this
	def count_down(n):
		while n > 0:
			n -= 1
			
	count_down(100000)
	
	# ('count_down', 0.006999969482421875)
	
当你写如下代码时：  

	@time_this
	def count_down(n):

意味着你分开执行了以下步骤：  
	
	@time_this
	def countdown(n):
	...
	count_down = time_this(count_down)
	
装饰器函数中的代码创建了一个新的函数（正如此例中的wrapper函数），它用\*args和\*\*kwargs接收任意的输入参数，
并且在此函数内调用原函数并且返回其结果。你可以根据自己的需要放置任何额外的代码（例如本例中的计时操作），新创建的包装函数将作为结果返回并取代原函数。  

	@decorator
	def function():
		print("inside function")
		
当编译器查看以上代码时，function()函数将会被编译，并且函数返回对象将会被传给装饰器代码，装饰器将会在做完相关操作之后用一个新的函数对象代替原函数。  

装饰器代码是什么样的？大部分的例子都是将装饰器定义为函数，而我发觉将装饰器定义成类更容易理解其功能，并且这样更能发挥装饰器机制的威力。  

对装饰器的类实现唯一要求是它必须能如函数一般使用，也就是说它必须是可调用的。所以，如果想这么做这个类必须实现__call__方法。  

这样的装饰器应该用来做什么？它可以做任何事，但通常它用在当你想在一些特殊的地方使用原函数时，但这不是必须的，例如：　　

	class decorator(object):
		def __init__(self, f):
			print("inside decorator.__init__()")
			f()  # Prove that function definition has completed.
			
		def __call__(self):
			print("inside decorator.__call__()")
			
	@decorator
	def function():
		print("inside function()")
		
	print("Finished decorating function()")
	
	function()
	
	# inside decorator.__init__()
	# inside function()
	# Finished decorating function()
	# inside decorator.__call__()
	
译者注：  
1. 语法糖@decorator相当于function=decorator(function),在此调用decorator的__init__打印"inside decorator\.\_\_init\_\_()"  
1. 随后执行f()打印"inside function()"  
1. 随后执行"print("Finished decorating function()")"  
1. 最后在调用function函数时，由于使用装饰器包装，因此执行decorator的__call__打印"inside decorator\.\_\_call\_\_()"。  

一个更实际的例子：  

	def decorator(func):
		def modify(*args, **kwargs):
			# 弹出对应key的value值
			variable = kwargs.pop('variable', None)
			print(variable)
			x, y = func(*args, **kwargs)
			return x, y
		return modify
		
	@decorator
	def func(a, b):
		print(a**2, b**2)
		return (a**2, b**2)
		
	func(a=4, b=5, variable="hi")
	func(a=4, b=5)
	
	# hi
	# 16 25
	# None
	# 16 25
