概念区分
------------------------------------

iOS中assign、copy 、retain等关键字的含义:
http://www.2cto.com/kf/201205/133943.html

Nonatomic

nonatomic is used for multi threading purposes. 
If we have set the nonatomic attribute at the time of declaration, 
then any other thread wanting access to that object can access it 
and give results in respect to multi-threading.

Copy

copy is required when the object is mutable. 
Use this if you need the value of the object as it is at this moment, 
and you don't want that value to reflect any changes made by other owners of the object. 
You will need to release the object when you are finished with it because you are retaining the copy.

Assign

Assign is somewhat the opposite to copy. 
When calling the getter of an assign property, it returns a reference to the actual data. 
Typically you use this attribute when you have a property of primitive type (float, int, BOOL...)

Retain

retain is required when the attribute is a pointer to an object. 
The setter generated by @synthesize will retain (aka add a retain count to) the object. 
You will need to release the object when you are finished with it. 
By using retain it will increase the retain count and occupy memory in autorelease pool.

Strong

strong is a replacement for the retain attribute, 
as part of Objective-C Automated Reference Counting (ARC). 
In non-ARC code it's just a synonym for retain.

This is a good website to learn about strong and weak for iOS 5. 
http://www.raywenderlich.com/5677/beginning-arc-in-ios-5-part-1

Weak

weak is similar to strong except that it won't increase the reference count by 1. 
It does not become an owner of that object but just holds a reference to it.
If the object's reference count drops to 0, even though you may still be pointing to it here, 
it will be deallocated from memory.

The above link contain both Good information regarding Weak and Strong.


Objective-C中的@property和@synthesize用法:
http://justcoding.iteye.com/blog/1444548

结论：@property相当于setter/getter接口方法声明，@synthesize相当于接口自动实现；

iOS开发之protocol和delegate:
http://blog.csdn.net/mars2639/article/details/7310182
http://www.cnblogs.com/qingjoin/archive/2012/11/22/2782602.html

结论：@protocol 相当于（定义为）一个接口类，而这个接口类实例化为一个delegate属性；

示例代码
-------------------------------------------
    @interface ViewController : UIViewController
    {
        // 不使用 @synthesize 只在这里写表示这个属性是私有属性
        // 不断给它赋值时不会改变引用计数
        NSString *str_;
        NSString *str;
    }

    // 不使用 @synthesize 只在这里写表示这个属性是公有属性
    // 不断给它赋值时会根据 retain assign copy 改变引用计数
    @property(nonatomic,retain)NSString *str;

    // 两个一起写名字相同需要使用 @synthesize str ＝ _str; 合成
    // 私有属性赋值：str_ ＝ nil;
    // 公有属性赋值：self.str = nil; 或 _str = nil; 如果合成了可以直接 str = nil;(不过 retain assign copy 会无效)
    // 属性名加前_表示公有属性，在 @property 声明时系统会自己加
    // 属性名加后_表示私有属性，这只是为了好看区分可以随意
    // 现在开启 Xcode 5.0 以上都开启了 ARC 用什么类型的属性就在哪声明就好了 不用在意内存释放
    @end

    @implementation ViewController
    @synthesize str = _str;
    @end

