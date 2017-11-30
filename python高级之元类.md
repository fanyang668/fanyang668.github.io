## 元类（MetaClasses）
元类提供了一个改变Python类行为的有效方式。  

元类的定义是”一个类的类“。任何实例是它自己的类都是元类。  

	class Demo(object):
		pass
		
	obj = Demo()
	
	print("Class of obj is {0}".format(obj.__class__))
	print("Class of Demo is {0}".format(Demo.__class__))
	
	# Class of obj is <class '__main__.Demo'>
	# Class of Demo is <type 'type'>
	
在上例中，我们定义了一个类Demo，并且生成了一个该类的对象obj。首先，可以看到obj的__class__是Demo。
有意思的来了，那么Demo的class又是什么呢？可以看到demo的__class__是type。  

所以说type是python类的类，换句话说，上例中的obj是一个Demo的对象，而Demo本身又是type的一个对象。  

所以说type就是一个元类，而且是python中最常见的元类，因为它是python中所有类的默认元类。  

因为元类是类的类，所以它被用来创建类（正如类是被用来创建对象的一样）。
但是，难道我们不是通过一个标准的类定义来创建类的么？的确是这样，但是python内部的运作机制如下：  

* 当看见一个类定义，python会收集所有属性到一个字典中。  
* 当类定义结束，python将决定类的元类，我们就称它为Meta吧。  
* 最后， python执行Meta(name, bases, dct)，其中：  

a. Meta是元类， 所以这个调用是实例化它。  
b. name是新建类的类名。  
c. bases是新建类的基类元组。  
d. dct将属性名映射到对象，列出所有的类属性。  

那么如何确定一个类（A）的元类呢？简单来说，如果一个类（A）自身或其基类（Base_A）之一有__metaclass__属性存在，则这个类（A/Bases_A）就是类（A）的元类。
否则type就将是类（A）的元类。  


## 模式（Patterns）
”请求宽恕比请求许可更容易（EFAP）“  

这个python设计原则是这么说的"请求宽恕比请求许可更容易（EFAP）"。
不提倡深思熟虑的设计思路，这个原则是说应该尽量去尝试，如果遇到错误，则给予妥善处理。
Python有着强大的异常处理机制可以支持这种尝试，这些机制帮助程序员开发出更为稳定，容错性更高的程序。  
