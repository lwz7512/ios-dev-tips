ios development tips for newies 
======================================
this is my daily records in ios development, learned one then write down one... 

### @2015/05/04 
* [1]. UI控件如何在源代码中引用：  
    点击show assistant editor按钮，打开辅助编辑器，在编辑器中打开view controller文件.h/.m  
    在Document outline中选中控件，按住ctrl键，拖拽到view controller中的@interface代码块内；  
    松开手指，弹出outlet connection对话框，在输入框中输入新生成的控件实例名称，回车确定；  
    如果是在.h中添加实例，则实例是public，如果是在.m的@interface代码块内添加实例，则实例是private的；  
    
* [2]. UI控件如何添加交互动作：  
    先在.h中添加 -(IBAction)eventHandlerName;  
    然后在.m中添加响应动作的实现 - (IBAction)eventHandlerName {}；  
    在Document outline中选中控件，打开connection inspector面板；  
    在sent events选择一个事件，按住事件后面的加号，拖拽到控件所属的view controller上松手；  
    在弹出的响应动作菜单中，选择刚才新加的动作；  
    
* [3]. 如何将toolbar控件中的bar button item居中：  
    设定bar button item的width，然后在item的两边各放置一个Flexible space bbi;  
    
### @2015/05/06/  

> 苹果IPHONE 5/5s屏幕分辨率：1136×640  
  [1] iPhone 6 Plus 采用标准的 1920×1080分辨率屏幕，PPI值为401；  
  [2] iPhone 6 则采用了1334×750分辨率的屏幕，PPI值为326。  
  显然，iPhone 6 Plus显示效果比iPhone 6好很多。  

* [4]. 如何为源码中的outlet连接到UI控件：  
    当.h代码中添加outlet比如：@property (nonatomic, strong) IBOutlet MKMapView *mapView;  
    而且.m中添加了实现比如@synthesize mapView;  
    则可以通过按住ctrl键，拖拽view controller图标到storyborad上的ui control对象上释放；  
    选择弹出列表已定义的outlet实例即可；  
    
> Q1: 如何让UI控件自适应iphone5, iphone6不同大小屏幕?  
 故事板中的控件均应该添加丢失的约束，这样不至于下次打开工程时法师控件失踪事件。。。  
 在toolbar中的控件没法通过约束自适应，只能通过flexible space bbi & fixed space bbi;  
 暂时无法通过IB来控制应用界面适配iphone5和iphone6....
    
* [5].  如何修改navigation item中的返回标题：  
    当view controller嵌入navigation controller后，当前的vc就有了标题栏(Navigation Item)；  
    标题栏内左边默认的的返回方式是< Back，当选中这个标题栏，然后在属性面板中可以添加Title和BackButton中的文字来修改；  
    
    

