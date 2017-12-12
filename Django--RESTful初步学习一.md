## REST是什么？
在网上能找到很多的资料，但是大多的REST相关的资料都显得晦涩难懂。
其实这也不怪那些作者，因为REST这个名字就很让人感觉到头痛。让我们来慢慢梳理下这个重要概念。  

REST 是用来干什么的？
REST 这个晦涩的概念如同其它计算机概念一样，
有的时候我们根本不知道它到底是怎么一回事，
但是我们却可以熟练的使用它。最典型的例子就是，
虽然我们大家都在写 Django ，
但是又有多少人能清楚的解释 MTV 模式是什么呢？
这就像是做数学题，虽然我不明白解方程中的换元思想，
但是我在不知不觉中就用到了它。
当我们提到 REST 的时候，后面通常会跟一个词——API。
所以在一般的概念里，
大家都把 REST 作为一种 API 的设计规范来理解。
所以 REST 就是用来设计 API 的吗？至少到目前为止，
我们所了解的 REST 就是用来设计 API 的。
它规定了一堆很烦人的规矩，让你去遵守它的规则，
把你的代码约束在一个固定的格式里。甚至在有的公司里，
他们对 REST 的态度是完全不理睬的。好吧，这是人的天性，
不喜欢被各种规矩所束缚，也不能怪他们。
正如我不喜欢按时起床一样，虽然起得来，
但是我就是想要躺在床上。
感觉自己冥冥之中在和什么东西作斗争。
我们在编写 API 的时候也在作斗争，
想要清晰明确的表达 API 的语义，又不想将代码写的太繁琐。
有的时候为了解析参数，如果设计不当，
你还会不得不自己手写一个 parser 来解析你的 URL 参数。
真是烦人。  

REST 就是将我们从灾难中解救出来的东西。
现在让我们来正式的认识一下它。REST ，
全称是 Representational State Transfer，中文翻译是：
资源的表现层状态转换。好了，
我想你看到这第一句就已经不想看了。WTF！
感觉中文都不通啊，这还理解个什么？？？淡定淡定。
仅仅是为了尊重下将这个概念提出来的作者 Roy Felding ，
他在他的论文《基于网络的软件架构》 中提出了这个概念。
我也不打算把这个概念解释给你听。我对于学习的哲学是：
知识的习得来源于知识对你的启发。所以，
我会带着大家来探索下，这个概念是个什么东西。
现在，请你忘记 REST 这个概念。 
忘记你曾经对 REST 的任何了解。  

假设你是个仓库管理员，管着一个巨大的仓库。
不仅看守着大门，还管理着从库的进进出出，
虽然仅仅是个小小的管理员，
但你已经俨然是个仓库经理的样子了。为了更好的管理仓库，
你决定，每个进来拿货的人，都必须出示相关的凭证。
凭证上必须有身份证明，如果你是来取货，
那就还必须要有取货证明，如果是来运货，那就必须有运货证明。
你每天守在大门前，兢兢业业的工作，但是却发现，
随着生意到了旺季，每天来来往往的人多起来，
你一个人恨不得分身成 8 个，4 个负责管进货的，4 个管出货的。
仓库门前那惟一一条路都快被来往的汽车车轮上的泥给染成黄色了。
累得够呛。感觉身体透支了。你必须想办法解决下这个问题。  

为了能够快速的检查凭证，你在仓库入口的最前面搭了个小棚，
专门检查他们的凭证。而且，为了节约时间，
不让他们一拿就拿一堆资料出来，
你规定所以的凭证相关信息都必须分门别类的写到一张纸上。
你现在只看他们一张纸！是的，管理员就是可以为所欲为，
通过了验证就盖个章；等他们凭证检查通过之后，
再根据他们凭证上提供的信息，看看他们是要干什么。
你多开了两个仓库进出口，进货的人就从左边走，
出货的从右边走，来打理仓库的从中间走。
不让他们都挤到一条路上。统一从后门出去。
进货的顺着左边那条路只能到一个空空的仓库间，
供给他们卸货；出货的顺着右边的路只能到一个小小的出货间，
他们把车后面的仓库门对准出货间的出口，
货物就会顺着流水线自己划到他们的车上。当然，
哪些货物可以被运到车上都是由在门口小棚的你来通过电脑全权控制的。
打理仓库的人只能进到自己的仓库间，
随便他们在仓库间里做什么，做完了就从后门走；
所有的货物都用大纸箱包装，进行统一的管理。
这样，你每天就坐在小棚里，既没有以前那没累了，
工作也更加的有条理。效率提高了一大截。  

这个小故事编的有些蹩脚，不过它还是完美诠释了对于 REST 的理解。
我们的数据库就是小故事中的仓库，而 URL 就是我们的大门。
在以前，对数据库做增加或者修改的操作都是由 POST 来完成的。
正如你改革仓库之前的那样，大家都走一条路。 
在改革之后，大家各走各的路。 我们的 URL 也需要各走各的路。
往数据库增加东西，请你用 POST 方法请求，修改请你用 PUT 方法来访问。
查询数据库，请你用 GET 请求。
当然，最重要的是，把凭证都写到一张纸上。
这张纸是什么呢？就是我们的请求头，
请不要 POST 里面有你的 UserAgent 信息，
也不要把你的验证信息放在 POST 里，把你是谁，你想干什么，
你的权限有哪些都放到请求头里。
好让我一看你的请求头就知道你要干什么。  

到这里，你可能还是会没多大感觉。不就是 POST 增加, 
PUT 修改， GET 获取详细信息吗？
看看我们在故事里还遗漏了什么？那就是我们多开了出口。
出口是什么？就是个管进出的大门吗？请你换种思维。
进出口，也是一种资源。进出口也是你管理的众多资源之一。
同样的道理，请求头也是资源。
你修路增加进出口，是在改变“进出口”这个资源，
你给凭证上面盖个章，是在改变凭证这个资源。
所以，URL 的 Header 也是资源。在用户访问一次之后，
你给用户的 cookie 做变动的时候，
就是在改变 cookie 这个资源。
当你决定用 PUT 来修改资源的时候，
是在改变请求方式这个资源。 不仅仅只有数据库是资源。
把仓库里的货物规定统一用大纸箱包装，
不管这些货物原来是什么样子，
在他们从仓库里运出来的时候看到的就是一个个个大纸箱。
统一他们的规格。我们的 API 也是同理，
不管你后端的资源是什么形式，我可以用 JSON ，
可以用 XML 来表示他们。
这些资源可能原来是在数据库里的二进制数据，
也可能是文本文档，也可能是一个 excel 表格。
但是当他们被展示在前端时，
他们都统一转化为了一模一样的形式。  

所以REST是什么，REST是一套对资源进行操作和展示的规范。这套规范虽然出生于一篇关于网络的论文，但是这并不妨碍将它运用到仓库管理上。  

## 设计API
在了解REST的核心概念————一切皆资源之后，让我们来看看，它是怎么具体运用到API上的。  
很简单，就以下几个点。  
* 一切皆是资源。不仅仅是对数据库的请求时资源。包括网页中的图片，音乐，cookie，session都是资源。  
* 展示资源。原来的资源可能是表格，可能是文本。但是可以用XML，JSON等方式来展示他们。  
* 每一个资源的每一个状态都应该有唯一的操作方式。  
	* POST增加资源
	* GET请求资源
	* PUT修改资源
	* DELETE删除资源
	
所以，资源——视一切为资源，
展示——不管资源原来是什么形式，可以用 XML、JSON 等来展示他们，
状态——被增加、被修改、被查看、被删除。
连起来就是 资源的表现层状态转换。这下就清晰多了。  

在API的设计共识里，我们的API应该包含以下几点：  
* 版本信息。让API的使用者清晰的知道使用的API是什么版本。  
* 使用名词的复数形式。比如： http://example.com/users/  
* 请求动词分工明确。GET就仅仅是请求资源，不会对被请求的资源有任何影响。POST就是增加资源，不能修改资源。  
* 命名规范统一，不能混用。  
	* 驼峰式。http://www/example.com/oldMan/  
	* 蛇形。http://www.example.com/old_man/  
* 内容协商。内容协商就是，用户希望以什么形式来展现资源。可以使JSON、XML、IMAGE，也可以是text。  
* 请求的所有元信息都放在请求头。  
* 当有其他资源动作时，在不违背基本的资源操作前提下，以URL参数的形式传递动作。比如：http:///www.example.com/users/?age=18&sex=girl  
* 返回正确的状态信息。比如大家最常见的404。  

根据以上知识，我们将要为我们的在线Python解释器应用设计API。  
其中，<arguement>代表URL参数arguement。  

* 添加代码：  
	* POST /v1/codes/
* 获取所有code实例：  
	* GET /v1/codes/  
* 获取指定code实例：  
	* GET /v1/codes/<pk>/  
* 修改指定code实例：  
	* PUT /v1/codes/<pk>/  
* 删除指定code实例：  
	* DELETE /v1/codes/<pk>/
* 运行代码：  
	* POST /v1/codes/run/  
	为什么用POST?因为运行代码也是向后台传送新的代码资源的方式  
* 运行特定代码实例：  
	* GET /v1/codes/run/<pk>/  
* 运行并保存代码实例：  
	* POST /v1/codes/run/?save=true  
* 修改并运行特定代码实例：  
	* PUT /v1/codes/run/<pk>/?save=true  
	
要是用Django的方式把我们的URL写出来的话，就是这个样子：  

	code_api = [
    url(r'^$', generic_code_view, name='generic_code'),  # code 集合操作
    url(r'^(?P<pk>\d*)/$', detail_code_view, name='detail_code'),  # 访问某个特定对象
    url(r'^run/$', run_code_view, name='run_code'),  # 运行代码
    url(r'^run/(?P<pk>\d*)/$', run_code_view, name='run_specific_code')  # 运行特定代码
	]
	api_v1 = [url('^codes/', include(code_api))]  # API 的 v1 版本
	api_versions = [url(r'^v1/', include(api_v1))]  # API 的版本控制入口 URL
	urlpatterns = [url(r'^api/', include(api_versions))],  # API 访问 URL
	
感觉 URL 的复杂度一下子就提升了不少。
淡定，仔细看看它的结构，这样的结构随时可以供我们随时进行修改。
比如，我们的API升级换代了，随时可以添加一个 api_v2 版本进去，
而不用去硬编码的修改原来的 API 。
这样既可以做到向后兼容，也可以方便的拓展。  

## 开发应用
### 前期的知识准备
上部分指挥讲解最基本的技术和知识，正式的动手写代码会在下部分进行。  

### Mixin
Mixin 技术是面向对象编程的一个重要技能。
它使得代码的结构更加灵活，提高了代码的复用性。
在实现一个功能时，根据需要的 Mixin 搭积木就好了，特别的方便。
在我们的应用中，我们将会大量的使用 Mixin 技术，并且，
Mixin 技术在 Django 中也被频繁的应用。
所以掌握 Mixin 是很必要的。
Mixin 技术能够产生，还是得益于对象的可继承性。  

比如我有一个对象叫做Man:  

	class Man:
		def __init__(self, name, age, height):
			self.name = name
			self.age = age
			self.height = height
			
我想让他会抽烟，于是我写了个抽烟Mixin：  

	class SmokeMixin:
		def smoke(self):
			print('饭后一支烟，赛过活神仙！')
			
我想让他会挣钱，于是写了个挣钱Mixin：  

	class MakeMoneyMixin:
		def make_money(self):
			print('面向工资编程中')
			
我想让他有个老婆：  

	class WifeMixin:
		wife = None
		def get_a_wife(self):
			return '我的老婆叫{}'.format(self.wife)
			
最后，这个Man成了这样的人：  

	class MyMan(SmokeMixin, WifeMixin, MakeMoneyMixin):
		wife = '王翠花'
		
	my_man = MyMan(name='老王', age=30, height=170)
	my_man.smoke()  # 饭后一支烟，赛过活神仙！
	my_man.make_money()  # 面向工资编程中
	my_man.wife()  # 我的老婆叫王翠花
	
但是每个男人都是不同的，因为有的男人也单身：  

	class SingleMan(SmokeMixin, MakeMoneyMixin):
		pass
		
	single_man = SingleMan(name='老李', age=25, height=165)
	single_man.smoke()  # 饭后一支烟，赛过活神仙！
	single_man.make_money()  # 面向工资编程中
	
这样我们就可以创造出很多个不同的男人，他们有相同点，我们要做的仅仅是把Mixin积木打上去。
我们的第二个男人的定义甚至只有一个pass。这种写法在大型工程里非常常见，只有一个pass，但是却有着丰富的功能。我们项目的视图就使用了Mixin技术：  

	class APICodeView(APIListMixin,  # 获取列表
				      APIDetailMixin,  # 获取当前请求实例详细信息
					  APIUpdateMixin,  # 更新当前请求实例
					  APIDeleteMixin,  # 删除当前实例
					  APICreateMixin,  # 创建新的实例
					  APIMethodMapMixin,  # 请求方法与资源操作方法映射
					  APIView):  # 记得在最后继承APIView
		model = CodeModel  # 传入模型
		
		def list(self):  # 这里仅仅是简单的给父类的list函数传参
			return super(APICodeView, self).list(fields=['name'])
			
这已经是 CodeAPI 完整代码了，
我们并没有在视图中手动的编写功能，
只是简单的继承了 Mixin ，
我们甚至都没有写 get，post, 等方法，在 Mixin 中也没有写！
这些神奇的功能和特性都是由 Mixin 提供的。  

## 状态
这是前端的知识点。在大家编写前端的时候，
一定要把逻辑思维转换为视觉思维。比如，
当你看到一盏灯亮了的时候，你的第一反应一定是“灯亮了”，
而不是“电流通过导线，让灯丝发热发光了”。
你看到一辆汽车从静止变成了运动的状态，
你不可能想到的是“摩擦力反作用于车轮让汽车动了起来”。
所以，当页面中的 UI 发生变化时，变化的是 UI 的状态。
一盏灯有熄灭和点亮两种状态，一辆车有发动和静止的状态，
一个人有吃饭，睡觉，走路等状态。拿我们应用中的表格来说，
它的状态就是有多少行。比如，原来只有 5 行，
你添了一行上去，就变成了 6 行，
此时这张表格从有 5 行的状态变成了 6 行的状态。 
这就是状态。
UI 的状态，就是它的样子，
UI 的样子是由它相关联的数据决定的。
这是很重要的概念，
在我们编写我们项目的前端时会发挥巨大作用。  


## 设计项目
在第一章，不管是在前端还是在后端开发，
我们在写代码之前都有设计的过程，同样的，
在这里我们也需要设计好我们的项目才可以开始写代码。  

## 需求分析
后端开发的主职责是提供 API 服务，同时，
我们不能再把 javascript 写在 html 里了，
因为这次的 javascript 代码会有点多，
所以我们要提供静态文件服务。一般来说，
静态文件服务都是由专门的静态文件服务器来完成的，
比如说 CDN ，也可以用 Nginx 。在这一章，我们的项目非常小，
所以就使用 Django 来提供静态文件服务。
我们计划自己编写一个简易的静态文件服务。  

## 项目结构
我们的项目结构如下：  

	online_interpreter_project/
		frontend/  # 前端目录
			index.html
			css/
				...
			js/
				...
		online_interpreter_project/  # 项目配置文件
			settings.py
			urls.py
			...
		online_intepreter_app/  # 我们真正的应用在这里
			...
		manage.py
		
大家可以看到，其实这一次，我们还是以后端为主，
前端并没有独立出后端的项目结构，就像刚才所说，
静态文件，或者说是前端文件，
应该尽量由专门的服务器来提供服务，
后端专门负责数据处理就可以了。  
做个深呼吸，开始动手了。

## 后端开发
在终端中新建一个项目： 

	python djnago-admin.py startproject online_intepreter_project
	
在这之前，我们使用的都是单文件的 Django ，
这一次我们需要使用 Django 的 ORM ，
所以需要按照标准的 Django 项目结构来构建我们的项目。
然后切换到项目路径内，建立我们的 app：  

	python manage.py startapp online_intepreter_app/
	
同时，将不需要的文件删除，并且再新建几个空文件。按照如下来修改我们的项目结构：  

	online_intepreter_project/
    frontend/ # 前端目录
        index.html
        css/
            bootstrap.css
            main.css
        js/
            main.js
            bootstrap.js
            jquery.js
    online_intepreter_project/ # 项目配置文件
        __init__.py
        settings.py # 项目配置
        urls.py # URL 配置
    online_intepreter_app/ # 我们真正的应用在这里
        __init__.py
        views.py # 视图
        models.py # 模型
        middlewares.py # 中间件
        mixins.py # mixin
    manage.py

编辑项目的settings.py：  

	import os

	BASE_DIR = os.path.dirname(os.path.dirname(os.path.abspath(__file__)))

	SECRET_KEY = '=@_j0i9=3-93xb1_9cr)i!ra56o1f$t&jhfb&pj(2n+k9ul8!l'

	DEBUG = True

	INSTALLED_APPS = ['online_intepreter_app']

	MIDDLEWARE = ['online_intepreter_app.middlewares.put_middleware']

	ROOT_URLCONF = 'online_intepreter_project.urls'

	DATABASES = {
		'default': {
        'ENGINE': 'django.db.backends.sqlite3',
        'NAME': os.path.join(BASE_DIR, 'db.sqlite3'),
		}
	}

INSTALLED_APPS:安装我们的应用。Django会遍历这个列表中的应用，并在使用makemigrations
这个命令时才会自动的搜寻并创建我们应用的模型。  

MIDDLEWARE:我们需要使用的中间件。由于Django不支持对PUT方法的数据处理，所以我们需要写一个中间件来给它加上这个功能。之后我们会更加详细的了解中间件的写法。  

DATABASES:配置我们的数据库。在这里，我们只是简单的使用了sqlite3数据库。  

以上便是所有配置了。  

现在我们先来编写 PUT 中间件，来让 Django 支持 PUT 请求。
我们可以使用 POST 方法向 Django 应用上传数据，
并且可以使用 request.POST 来访问 POST 数据。
我们也想像使用 POST 一样来使用 PUT ，
利用 request.PUT 就可以访问到 PUT 请求的数据。  

中间件是 django 很重要的一部分，
它在请求和响应之间充当预处理器的角色。
很多通用的逻辑可以放到这里，django 会自动的调用他们。
在这里，我们写了一个简单的中间件来处理 PUT 请求。
只要是 PUT 请求，我们就对它作这样的处理。所以，
当你对某个请求都有相同的处理操作时，可以把它写在中间件里。
所以，中间件是什么呢？
中间件只是视图函数的公共部分。
你把中间件的核心处理逻辑复制粘贴到视图函数中也是能够正常运行的。  

打开你的middlewares.py:  

	from django.http import QuerDict
	
	def put_middleware(get_response):
		def middleware(request):
			if request.method == 'PUT':
				# 给请求设置PUT属性，这样我们就可以在视图函数里面访问这个属性了
				setattr(request, 'PUT', QueryDict(request.body))
				# request.body是请求的主体。我们知道请求头，那请求的主体就是request.body了
				# 当然，你一定还会问，为什么这样就可以访问PUT请求的相关数据了呢？
				# 这涉及到了http协议的知识，这里就不展开了，有兴趣的同学可以自行查阅资料
			response = get_response(request)  # 使用get_response返回响应
			return response  # 返回响应
				
		return middleware  # 返回核心的中间件处理函数
		
QueryDict 是 django 专门为请求的查询字符串做的数据结构，
它类似字典，但是又不是字典。
request 对象的 POST GET 属性都是这样的字典。
类似字典，是因为 QueryDict 和 python 的 dict 有相似的 API 接口，
所以你可以把它当字典来调用。  

不是字典，是因为 QueryDict 允许同一个键有多个值。
比如 {'a':[‘1’,‘2’]}，a 同时有值 1 和 2，所以，
一般不要用 QueryDict[key] 的形式来访问相应 key 的值，
因为你得到的会是一个列表，而不是一个单一的值，
应该用 QueryDict.get(key) 来获取你想要的值，
除非你知道你在干什么，你才能这样来取值。
为什么会允许多个值呢，因为 GET请求中，
常常有这种参数 http://www.example.com/?action=search&action=filter ，
action 在这里有两个值，有时候我们需要对这两个值都作出响应。
但是当你用 .get(key)方法取值的时候，只会取到最新的一个值。
如果确实需要访问这个键的多个值，应该用 .getList(key) 方法来访问，
比如刚才的例子应该用 request.GET.getList('action') 来访问 action 的多个值。  

同理，对于POST请求也应该这么做。  

接下来要说说 request.body 。做过爬虫的同学一定都知道，
请求有请求头，那这个 body 就是我们的请求体了。严格的讲，
这个“请求体”应该叫做“载荷”，用英文来讲，
这就叫做“payload”。载荷里又有许多的学问了，
感兴趣的同学可以自己去了解相关的资料。
只需要知道一件很简单的事情，
就是把 request.body 放进 QueryDict 就可以把上传的字段转换为我们需要的字典了。  

由于原生的 request 对象并没有 PUT 属性，
所以我们需要在中间件中加上这个属性，
这样我们就可以在视图函数中用 request.PUT 来访问 PUT 请求中的参数值了。

中间件在 1.11 版本里是一个可调用对象，
和之前的类中间件不同。既然是可调用对象，那就有两种写法，
一种是函数，因为函数就是一个可调用对象；
一种是自己用类来写一个可调用对象，也就是包含 __cal__() 方法的类。  

在 1.11 版本中，中间件对象应该接收一个 get_response的参数，
这个参数用来获取上一个中间件处理之后的响应，
每个中间件处理完请求之后都应该用这个函数来返回一个响应，
我们不需要关心这个 get _response 函数是怎么写的，
是什么东西，只需要记得在最后调用它，返回响应就好。
这个最外层函数应该返回一个函数，用作真正的中间件处理。  

在外层函数下写你的预处理逻辑，比如配置什么的。当然，
你也可以在被返回的函数中写配置和预处理。
但是这么做有时候就有些不直观，配置、预处理和核心逻辑分开，
让看代码的人一眼就明白这个中间件是在做什么。
最通常的例子是，很多的 API 会对请求做许多的处理，
比如记录下这个请求的 IP 地址就可以先在这里做这个步骤；
又比如，为了控制访问频率，可以先读取数据库中的访问数据，
根据访问数据记录来决定要不要让这个请求进入到视图函数中。
我们对 PUT 请求并没有什么预处理或者配置操作要进行，
所以就什么都没写。  

中间件的处理逻辑虽然简单，但是中间件的写法和作用大家还是需要掌握的。  

接下来，让我们创建我们的模型，编辑你的models.py:  

	from django.db import models
	
	# 创建Code模型
	class CodeModel(models.Model):
		name = models.CharField(max_length=50)  # 名字最长为50个字符
		code = models.TextField()  # 这个字段没有文本长度的限制
		
		def __str__(self):
			return 'Code(name={}, id={})'.format(self.name, self.id)
			
在这里要注意一下，如果你是 py2 ，__str__ 你需要改成 __unicode__ 。
我们的表结构很简单，这里就不多说了。  

我们的 API 返回的是 json　数据类型，
所以我们需要把最基础的响应方式更改为 JsonResponse 。
同时，我们还有一个问题需要考虑，
那就是如何把模型数据转换为 json 类型。 
我们知道 REST 中所说的 “表现（表层）状态转换” 就是这个意思，
把不同类型的数据转换为统一的类型，然后传送给前端。
如果前端要求是 json 那么我们就传 json 过去，
如果前端请求的是 xml 我们就传 xml 过去。
这就是“内容协商（协作）”。当然，我们的应用很简单，
就只有一种形式，但是如果是其它的大型应用，
前端有时请求的是 json 格式的，有时请求的是 xml 格式的。
我们的应用很简单，就不用考虑内容协商了。  

回到我们的问题，我们该如何把模型数据转换为 json 数据呢？
把其它数据按照一定的格式保存下来，这个过程我们称为“序列化”。
“序列化”这个词其实很形象，它把一系列的数据，
按照一定的方式给整整齐齐的排列好，保存下来，以便他用。
在 Django 中，Django 为我们提供了一些简单的序列化工具，
我们可以使用这些工具来把模型的内容转换为 json 格式。  

其中很重要的工具便是 serializers 了，
看名字我们就这到它是用来干什么的。
其核心函数 serialize(format, queryset[,fields]) 
就是用于把模型查询集转换为 json 字符串。
它接收的两个参数分别为 format，format 也就是序列化形式，
如果我们需要 json 形式的，我们就把 format 赋值为 'json' 。 
第二个参数为查询集或者是一个含有模型实例的可迭代对象，
也就是说，这个参数只能接收类似于列表的数据结构。
fields 是一个可选参数，他的作用就和 Django 表单中的 fields 一样，
是用来控制哪些字段需要被序列化的。  

编辑你的views.py:  

from django.views import View  # 引入最基本的类视图
from django.http import JsonResponse # 引入现成的响应类
from django.core.serializers import serialize  # 引入序列化函数
from .models import CodeModel  # 引入 Code 模型，记得加个 `.`  哦。
import json  # 引入 json 库，我们会用它来处理 json 字符串。

# 定义最基本的 API 视图
	class APIView(View):
		def response(self,
					queryset=None,
					fields=None,
					**kwargs):
			"""
			序列化传入的 queryset 或 其他 python 数据类型。返回一个 JsonResponse 。
			:param queryset: 查询集，可以为 None
			:param fields: 查询集中需要序列化的字段，可以为 None
			:param kwargs: 其他需要序列化的关键字参数
			:return: 返回 JsonResponse
			"""

			# 根据传入参数序列化查询集，得到序列化之后的 json 字符串
			if queryset and fields:
				serialized_data = serialize(format='json',
											queryset=queryset,
											fields=fields)
			elif queryset:
				serialized_data = serialize(format='json',
											queryset=queryset)
			else:
				serialized_data = None
			# 这一步很重要，在经过上面的查询步骤之后， serialized_data 已经是一个字符串
			# 我们最终需要把它放入 JsonResponse 中，JsonResponse 只接受 python 数据类型
			# 所以我们需要先把得到的 json 字符串转化为 python 数据结构。
			instances = json.loads(serialized_data) if serialized_data else 'No instance'
			data = {'instances': instances}
			data.update(kwargs)  # 添加其他的字段
			return JsonResponse(data=data)  # 返回响应
			
需要注意的是，我们先序列化了模型，然后又用json把它转换为了python的字典结构，
因为我们还需要把模型的数据和我们的其它数据(kwargs)放在一起之后才会把它变成真正的json数据类型。  

