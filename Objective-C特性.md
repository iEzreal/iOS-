##### 属性关键字
* `读写权限`
 * `readonly`
 
 * `readwrite(默认)`
 
* `原子性`
 * `atomic` 赋值&获取是线程安全的，其它则是非线程安全的
 
 * `nonatomic`
  
* `引用计数`
 * `retain/strong` 
 
	 ```
	 **面试题**
	 MRC下如何重写retain修饰变量的setter方法
	 - (void)setObj:(id)obj {
		  if (_obj != obj) {
		      [_obj release];
		      _obj = [obj retain];
		  }
	 }
	 
	 **分析不等判断的主要原因**
	 如果自身赋值：在调用release方法时，对象引用计数为0话，就会释放对象；在调用retain方法就会产生异常
	 ```
 
 * `assign` **基本数据类型** **修饰对象**
 
	 ```
	 * 修饰对象时，不改变被修饰对象的引用计数
	 * 对象在释放时，仍指向原地址
	 * 会产生悬垂指针
	 
	 ```

 * `weak` **修饰对象**
 
	 ```
	 * 不改变被修饰对象的引用计数
	 * 所指对象在被释放之后会自动置为nil
		
	 ```
 * copy
 
	 ```
	 * 可变对象的copy和mutableCopy都是深拷贝
	 * 不可变对象的copy是浅拷贝，mutableCopy是深拷贝
	 * copy方法返回的都是不可变对象
	 ```
	 ```
	 **面试题**
	 @property(nonatomic, copy)NSMutableArray *array ?
	 * 如果赋值过来的是NSMutableArray，copy之后是NSArray
	 * 如果赋值过来的是NSArray，copy之后是NSArray
	 ```

#### Category（分类）
Objective-C 2.0之后添加的语言特性，主要作用就是在不改变原有类的前提下，动态的给这个类添加一些方法。

* 底层实现原理
	
* 分类中可以添加哪些内容？
	* 实例方法
	* 类方法
	* 协议
	* 属性 该属性只是生成了setter和getter的方法声明，并没有产生对应的实现，更不会添加带下划线"_"的成员变量。
	
* 特点
	* 运行时决议
	* 可以为系统类添加分类


* 加载调用栈 

* 使用分类做了那些事？
	* 声明私有方法
	* 分解体积庞大的类文件
	* 把Framework的私有方法公开化


#### 关联对象
关联对象由AssociationsManager管理，并在AssociationsHashMap存储，
所有对象的关联内容都在**同一个全局容器**中

* 底层实现原理


* 能否给分类添加 **成员变量**？

```
/**
 * 关联对象
 *
 * @param object 被关联对象
 * @param key 关联的key
 * @param value 关联的值
 * @param policy 内存管理的策略
 *
 */
void objc_setAssociatedObject(id _Nonnull object, const void * _Nonnull key, id _Nullable value, objc_AssociationPolicy policy)
```

```
/**
 * 获取关联对象
 *
 * @param object 被关联的对象
 * @param key 关联对象的key
 *
 * @return 关联对象key对应的值
 *
 */
id _Nullable objc_getAssociatedObject(id _Nonnull object, const void * _Nonnull key)
```

```
/**
 * 移除关联的对象
 *
 * @param object 被关联的对象
 *
 */
void objc_removeAssociatedObjects(id _Nonnull object)
```


#### Extension（扩展）
类扩展(extension）是category的一个特例，有时候也被称为匿名分类。它的作用是为一个类添加一些私有的成员变量和方法。

* 特点
	* 编译时决议
	* 只以声明的形式存在，多数情况下寄生于宿主类的.m中
	* 不能为系统类添加扩展 

* 一般用扩展做什么？
	* 声明私有属性
	* 声明私有方法
	* 声明私有成员变量

#### Delegate（代理）
* 准确的说是一种**软件设计模式**
* iOS当中以@protocol形式体现
* 传递方式为一对一


#### NSNotification (通知)
* 使用**观察者模式**来实现，用于跨层传递消息的机制
* 传递方式为一对多

* 如何实现通知机制？
  


#### KVO


#### KVC