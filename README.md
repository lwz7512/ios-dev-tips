ios development tips for newies 
======================================
this is my daily records in ios development, learned one then write down one... 

### @2015/05/03

* :zap:[1]. __如何创建view controller?__:
    在工程中创建controllers组，然后在组上右键，New File... >  
    iOS/Source 选择Cocoa Touch Class, Next > Subclass of: UIViewController  
    Class: 中会自动填入ViewController，将光标定位在ViewController前面，输入新控制器名字，Next >  
    出现保存位置和指定归属组的对话框，什么都不用改，点Create，在controllers组下就生成了.h/.m文件  

### @2015/05/04 

* :zap:[2]. __UI控件如何在源代码中引用?__：  
    点击show assistant editor按钮，打开辅助编辑器，在编辑器中打开view controller文件.h/.m  
    在Document outline中选中控件，按住ctrl键，拖拽到view controller中的@interface代码块内；  
    松开手指，弹出outlet connection对话框，在输入框中输入新生成的控件实例名称，回车确定；  
    如果是在.h中添加实例，则实例是public，如果是在.m的@interface代码块内添加实例，则实例是private的；  
    
* :zap:[3]. __UI控件如何添加交互动作?__：  
    先在.h中添加 -(IBAction)eventHandlerName;  
    然后在.m中添加响应动作的实现 - (IBAction)eventHandlerName {}；  
    在Document outline中选中控件，打开connection inspector面板；  
    在sent events选择一个事件，按住事件后面的加号，拖拽到控件所属的view controller上松手；  
    在弹出的响应动作菜单中，选择刚才新加的动作；  
    
* :zap:[4]. __如何将toolbar控件中的bar button item居中?__：  
    设定bar button item的width，然后在item的两边各放置一个Flexible space bbi;  
    
### @2015/05/06/  

> 苹果IPHONE 5/5s屏幕分辨率：1136×640  
  [1] iPhone 6 Plus 采用标准的 1920×1080分辨率屏幕，PPI值为401；  
  [2] iPhone 6 则采用了1334×750分辨率的屏幕，PPI值为326。  
  显然，iPhone 6 Plus显示效果比iPhone 6好很多。  

* :zap:[5]. __如何为源码中的outlet连接到UI控件?__：  
    当.h代码中添加outlet比如：@property (nonatomic, strong) IBOutlet MKMapView *mapView;  
    而且.m中添加了实现比如@synthesize mapView;  
    则可以通过按住ctrl键，拖拽view controller图标到storyborad上的ui control对象上释放；  
    选择弹出列表已定义的outlet实例即可；  
    
* :zap:[6]. __如何让UI控件自适应iphone5, iphone6不同大小屏幕?__  
    故事板中的控件均应该添加丢失的约束，这样不至于下次打开工程时发生控件失踪事件。。。  
    在toolbar中的控件没法通过约束自适应，只能通过flexible space bbi & fixed space bbi;  
    ~~暂时无法通过IB来控制应用界面适配iphone5和iphone6~~....
    
* :zap:[7]. __如何修改navigation item中的返回标题?__：  
    当view controller嵌入navigation controller后，当前的vc就有了标题栏(Navigation Item)；  
    标题栏内左边默认的的返回方式是< Back，当选中这个标题栏，然后在属性面板中可以添加Title和BackButton中的文字来修改；  
    
    
### @2015/05/11

> 导航控制器命名规范：使用nav_为前缀，已区分其他view controller;  


### @2015/05/14

* :zap:[8]. __如何自定义视图组件？__: 
    创建一个components组，选中该组，按下cmd + n 弹出对话框：  
    New File... > iOS/Source, 选择 Cocoa Touch Class , Next > 输入新建的Class名称，指定 Subclass of: UIView , Next > 选择物理路径， Create  
    这样就生成了.h/.m文件，实现.m中的个别方法例如drawRect，就可以将此类指定给故事板上的视图了：  
    选定视图 > 切换到Identity inspector > Custom Class: Class下拉列表中找到刚才创建的类，这样就完成了视图自定义；  

* :zap:[9]. __如何让自定义视图在不变形的情况下水平居中？__:  
    垂直方向，距离顶部或者底部指定一个Vertical Space 约束就行，不能同时在该方向指定两个约束，否则垂直方向会被拉伸；  
    水平方向，指定一个Center X Alignment，即水平对齐，选中该约束，视图上会高亮显示一个垂直的轴线；  
    视图内部如果有控件的话，内部控件也要设置水平、垂直、水平居中、控件大小约束，可以根据建议来自动设置；  
    
    

### @2015/05/18

* :zap:[10]. __如何将[MBProgressHUD](https://github.com/jdg/MBProgressHUD)组件引入当前工程？__:
    MBProgressHUD是非常常用的进度条组件，引入步骤也非常简单，使用CocoaPods方式受GWF所限，这里只用源码方式：  
    在你的工程目录下`$ git clone https://github.com/jdg/MBProgressHUD.git`  
    xcode中打开你的工程，打开MBProgressHUD文件夹，从中拖拽MBProgressHUD.h和MBProgressHUD.m到你的工程视图目录树中  
    释放后在弹出窗口中确保选择Destination: Copy items if needed  
    在你的视图控制器中引入该组件：#import "MBProgressHUD.h"  
    
    
### @2015/05/19

* :zap:[11]. __如何在xcode工程中使用[CocoaPods](https://cocoapods.org/)进行库依赖管理__: 
    安装：`$ sudo gem install cocoapods`  
    安装后就可以使用pod命令了，首先要建立本地CocoaPods environment：`$ pod setup`  
    在xcode工程目录下创建一个[Podfile](https://guides.cocoapods.org/using/the-podfile.html)文件来管理依赖的库  
    在该文件中添加：
    pod 'AFNetworking', '~> 2.0'  
    pod 'ObjectiveSugar', '~> 0.5'  
    然后执行：`$ pod install`  
    这样依赖的库就下载到工程中了，如果该工程已经打开，则关掉，双击*.xcworkspace打开整合pod的新工程  
    如果添加新的依赖，则再添加一行pod 'libaray name'，然后：`$ pod install` or `$ pod update`  
    update命令会更新依赖库到最新版本，而install只按照配置文件中的版本去下载  
    如果以前是以源码方式引入库，再使用pod方式重新添加该库时，则要在工程视图中删掉拷贝进来的.h/.m文件，否则编译失败  
    报错说符号重复。。。因为重复引用了。。。
    
### @2015/05/22

* :zap:[12]. __Objective-C语言#import引入头文件时，.h和.m有什么区别？__:
  .h文件是头文件，包含了类，类型、函数与常数的声明；.m文件是源代码文件；在头文件导入.h可以确保相同的文件只会被包含一次，  
  而不会重复的导入相同类型的文件；而在.m文件导入，你就会发现在其他的头文件中可以同样导入相关联的文件，区别就在于这里;
  注：来自百度百科
  TODO: 还需进一步理解...
  
* :zap:[13]. __如何理解UIViewController lifecycle__:
  viewDidLoad -> ViewWillAppear:(BOOL)animated -> ViewDidAppear:(BOOL)animated -> ViewDidUnload -> ViewDidDispose
  参考：[这里](http://stackoverflow.com/questions/5562938/looking-to-understand-the-ios-uiviewcontroller-lifecycle)

* :zap:[14]. __IOS中延时执行的几种方式[比较和汇总](http://blog.sina.com.cn/s/blog_8280f5ec0101k03c.html)__:
  performSelector方法  
  定时器:NSTimer  
  sleep方式  
  GCD方式  

### @2015/05/26

* :zap:[15]. __如何为动态按钮或者列表项添加导航？__:
  动态创建的按钮或者table cell有时需要实现点击跳转功能，这就需要动态导航；  
  这时需要：  
  为目标view controller指定storyboard id，比如：conversation_view  
  然后通过代码创建该视图控制器实例：  
  `ConversationViewController *myVController = (ConversationViewController *)[self.storyboard instantiateViewControllerWithIdentifier:@"conversation_view"];`  
  最后完成导航：  
  `[self.navigationController pushViewController:myVController animated:YES];`  
  注意前提是当前视图控制器已经嵌入了导航控制器  

### @2015/05/26

* :zap:[16]. __xxx__:






