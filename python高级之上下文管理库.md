## 上下文管理库（ContextLib）
contextlib模块包含了与上下文管理器和with声明相关的工具。通常如果你想写一个上下文管理器，则你需要定义一个类包含__enter__方法以及__exit__方法，例如：  

	import time
	class demo:
	def __init__(self, label):
		self.label = label
		
	def __enter__(self):
		self.start = time.time()
		
	def __exit__(self, exc_ty, exc_val, exc_tb):
		end = time.time()
		print('{}: {}'.format(self.label, end-self.start))
		
完整的例子在此：  

	import time
	class demo:
	def __init__(self, label):
		self.label = label
		
	def __enter__(self):
		self.start = time.time()
		
	def __exit__(self, exc_ty, exc_val, exc_tb):
		end = time.time()
		print('{}: {}'.format(self.label, end-self.start))
		
	with demo('counting'):
		n = 1000000
		while n > 0:
			n -= 1
			
	# counting: 1.36000013351
	
上下文管理器被with声明所激活，这个API涉及到两个方法。  
1. \_\_enter__方法，当执行流进入with代码块时，__enter__方法将执行。并且它将返回一个可供上下文使用的对象。  
1. 当执行流离开with代码块时， __exit__方法被调用，它将清理被使用的资源。  

利用@contextmanager装饰器改写上面那个例子：  

	from contextlib import contextmanager
	import time
	
	@contextmanager
	def demo(label):
		start = time.time()
		try:
			yield
		finally:
			end = time.time()
			print('{}: {}'.format(label, end - start))
		
	with demo('counting'):
		n = 1000000
		while n > 0:
			n -= 1
			
	# counting: 1.32399988174
	
看上面这个例子，函数中yield之前的所有代码都类似于上下文管理器中__enter__方法的内容。
而yield之后的所有代码都如__exit__方法的内容。如果执行过程中发生了异常， 则会在yield语句触发。
