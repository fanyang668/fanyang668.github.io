在Python中，读写文件这样的资源要特别注意，必须在使用完毕后正确关闭它们。
正确关闭文件资源的一个方法是使用try...finally:  

	try:
		f = open('/path/to/file', 'r')
		f.read()
	finally:
		if f:
			f.close()
			
写try...finally非常繁琐。Python的with语句允许我们非常方便的使用资源，而不必担心资源没有关闭，
所以上面的代码可以简化为：  

	with open('/path/to/file', 'r') as f:
		f.read()
		
并不是只有open()函数返回的fp对象草能使用with语句。实际上，任何对象，只要正确实现了上下文管理，
就可以用于with语句。  

例如：  

	with context_expression [as target(s)]:
		with_body
		
它的执行顺序是这样的：  
1. 执行context_expression，生成上下文管理器context_manager；  
1. 调用上下文管理器的enter()方法；如果使用了as子句，则将enter()方法的返回值赋值给as子句中的target(s)；  
1. 执行语句体with_body；  
1. 不管执行过程中是否发生了异常，执行上下文管理器的exit()方法，exit（）方法负责执行“清理”工作，
如释放资源等。如果执行过程中没有出现异常，或者语句体中执行了语句break/continue/return，
则以None作为参数调用exit(None, None, None)；如果执行过程中出现异常，则使用sys.exc_info得到的异常信息为参数调用
exit(exc_type, exc_value, exc_traceback)；  
1. 出现异常时，如果exit(type, value, traceback)返回False，则会重新抛出异常，让with之外的语句逻辑来处理异常，
这也是通用做法；如果返回True，则忽略异常，不再对异常进行处理；  


实现上下文管理是通过__enter__和__exit__这两个方法实现的。例如，下面的class实现了这两个方法：  

	class Query(object):
		def __init__(self, name):
			self.name = name
		
		def __enter__(self):
			print('Begin')
			return self
			
		def __exit__(self, exc_type, exc_value, traceback):
			if exc_type:
				print('Error')
			else:
				print('End')
				
		def query(self):
			print('Query info about %s...' % self.name)
			
这样我们就可以把自己写的资源对象用于with语句：  

	with Query('Bob') as q:
		q.query()
		
## @contextmanager
编写__enter__和__exit__仍然很繁琐，因此Python的标准库contextlib提供了更简单的写法，上面的代码可以改写如下：  

	from contextlib import contextmanager
	
	class Query(object):
		def __init__(self, name):
			self.name = name
			
		def query(self):
			print('Query info about %s...' % self.name)
			
	
	@contextmanager
	def create_query(name):
		print('Begin')
		q = Query(name)
		yield q
		print('End')
		
@contextmanager这个decorator接受一个generator，用yield语句把with ... as var把变量输出出去，
然后，with语句就可以正常地工作了：  

	with create_query('Bob') as q:
		q.query()
		
很多时候，我们希望在某段代码执行前后执行特定到吗，也可以用@contextmanager实现。
例如：  

	@contextmanager
	def tag(name):
		print("<%s>" % name)
		yield
		print("</%s>" % name)
		
	with tag("h1"):
		print("hello")
		print("world")
		
	# <h1>
	# hello
	# world
	# </h1>
	
代码的执行顺序是：  
1. with语句首先执行yield之前的语句，因此打印出\<h1>；  
1. yield调用会执行with语句内部的所有语句，因此打印出hello和world；  
1. 最后执行yield之后的语句，打印出\</h1>。  
	
因此，@contextmanager让我们通过编写generator来简化上下文管理。
	
## @closing
如果一个对象没有实现上下文，我们就不能把它用于with语句。这个时候，可以用closing()来把该对象变为上下文对象。例如，
用with语句使用urlopen():  

	from contextlib import closing
	from urllib.request import urlopen
	
	with closing(urlopen('http://www.python.org')) as page:
		for line in page:
			print(line)
			
closing也是一个经过@contextmanager装饰的generator，这个generator编写起来其实非常简单：  

	@contextmanager
	def closing(thing):
		try:
			yield thing
		finally:
			thing.close()
			
它的作用就是把任意对象变为上下文对象，并支持with语句。  

@contextlib还有一些其他的decorator，便于我们编写更简洁的代码。  

