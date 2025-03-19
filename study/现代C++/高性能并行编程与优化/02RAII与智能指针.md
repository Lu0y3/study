## 现代C++入门
![alt text](image-15.png)

### C++11 14 17 20 初步了解
![alt text](image-16.png)
![alt text](image-17.png)
![alt text](image-18.png)

---
基于迭代器的，，像list这种的也能正常使用
![alt text](image-19.png)

---
for_each是一个模板函数 可以支持任何具有begin和end迭代器的容器

![alt text](image-20.png)

---
Lambda表达式
C++11引入
![alt text](image-21.png)
C++14 允许auto
![alt text](image-22.png)

---
vector< T>
C++17 CTAD编译期参数推断，如tuple \pair  就不需要make_pair帮手了
运行时没有额外开销
![alt text](image-23.png)

numeric
C++17引入常用数值算法
![alt text](image-24.png)

![alt text](image-25.png)

ranges
C++20引入区间
![alt text](image-26.png)

mudule
C++20引入模块
import <>
![alt text](image-27.png)

C++20函数参数为auto
![alt text](image-28.png)

C++20引入coroutine协程和generator生成器
![alt text](image-29.png)

C++20引入format
![alt text](image-30.png)


![alt text](image-31.png)

### C++有哪些面向对象思想？

#### 封装
![alt text](image-33.png)
![alt text](image-34.png)
![alt text](image-35.png)


#### RAII
##### 资源获取即初始化 
尽量不去使用new delete
![alt text](image-36.png)
##### 避免犯错
![alt text](image-37.png)
##### 异常安全
throw异常后会自动调用已创对象的析构
![alt text](image-38.png)
#### RAII离不开构造函数
![alt text](image-39.png)

---
无参构造 : 先初始化为空后又赋值 两次
![alt text](image-40.png)

---
初始化表达式 ：直接初始化
类成员的const一定要使用初始化表达式，因为避免const变量空初始化 后再拷贝赋值给一个const变量
![alt text](image-41.png)

---
多参构造
![alt text](image-42.png)

---
单参构造
![alt text](image-43.png)

---
单参隐式构造(陷阱)
![alt text](image-45.png)

---
单参显示构造(陷阱)
![alt text](image-44.png)

避免陷阱的体现
![alt text](image-46.png)

---
explicit对多参也有作用
![alt text](image-47.png)

---
使用{} 和 () 调用构造函数区别
{}需要避免变窄转换
![alt text](image-48.png)

---
默认构造 POD plain old data
![alt text](image-49.png)
解决POD陷阱方案
![alt text](image-50.png)

![alt text](image-51.png)

---
加 {} 进行零初始化 nullptr
   obj=  { ， }  右边相当于一个整体 进行隐式转换
   obj{ ， } 一个一个 个体
![alt text](image-52.png)

---
初始化列表 C++11 
![alt text](image-53.png)

C++20支持 指定名称跳顺序  要求所有数据成员public
![alt text](image-54.png)

---
CTAD 编译时参数推断
![alt text](image-55.png)

---
自定义构造函数后若还想要一个默认构造函数 ：=default
![alt text](image-56.png)

---
拷贝构造函数   区别于指向同一个对象 copy一个新的对象操作
![alt text](image-57.png)

---
![alt text](image-58.png)

---
=delete
![alt text](image-59.png)

---
拷贝赋值函数
![alt text](image-60.png)

返回 &   是为了支持链式等号 a=b=c

---
全家桶
拷贝默认都是深拷贝
智能指针是浅拷贝 最好只有智能指针采用
![alt text](image-61.png)
![alt text](image-62.png)

---
学废啦
![alt text](image-63.png)

---
##### 实现一个简单有问题的Vector类
![alt text](image-64.png)

---
##### 三五法则
![alt text](image-65.png)

---
1、定义了析构函数，则必须同时定义或删除 拷贝构造函数和移动构造函数 --若不，默认拷贝函数对指针进行浅拷贝，会析构free指针两次，资源释放两次，出错。
![alt text](image-66.png)
![alt text](image-67.png)

---
2、拷贝赋值函数
![alt text](image-68.png)

![alt text](image-69.png)

---
为什么区分拷贝和移动
移动拷贝 深拷贝
移动： 接管所有权 被移动的对象数据情况
![alt text](image-70.png)

---
移动
swap  move
![alt text](image-71.png)

---
![alt text](image-72.png)

---
记得写noexcept
![alt text](image-73.png)

---
构造函数总结
![alt text](image-74.png)

彻底学废了
![alt text](image-75.png)


### 内存管理
![alt text](image-76.png)

#### unique_ptr
![alt text](image-77.png)

new C 如果C是POD随机初始化内存    new C() 零初始化

封装:不变  一组操作时原子的要么全做要么全不做  且都是处于正确状态
##### 禁用拷贝
![alt text](image-78.png)

##### 只是对其操作
![alt text](image-79.png)

##### move它的所有权
![alt text](image-80.png)

##### move希望再次访问它
![alt text](image-81.png)

##### 提前获得原始指针 
![alt text](image-82.png)

##### 但不能在再次操作前删除它
![alt text](image-83.png)


---

#### shared_ptr
![alt text](image-84.png)

多线程需要去考虑sharedptr的原子性

![alt text](image-85.png)

##### 只要sharedptr?不要uniqueptr?  循环引用
![alt text](image-86.png)


#### weak_ptr不计数  解决循环引用

![alt text](image-87.png)

![alt text](image-91.png)
![alt text](image-90.png)


![alt text](image-88.png)

weaker.lock() 会+1 然后出作用域-1  本行？

![alt text](image-89.png)

---
C++ 中的对象都是深拷贝；只有sharedptr和weakptr是浅拷贝 而 uniqueptr则是禁止了拷贝 只有move移动
![alt text](image-92.png)

---
### 三五法则什么时候需要考虑
![alt text](image-93.png)

![alt text](image-94.png)

![alt text](image-95.png)

![alt text](image-96.png)

![alt text](image-97.png)

![alt text](image-98.png)

![alt text](image-100.png)

![alt text](image-101.png)

![alt text](image-102.png)


### 扩展
![alt text](image-103.png)


### 作业 
![alt text](image-104.png)

https://github.com/parallel101/hw02

#### 1.P-IMPL模式
PIMPL（Pointer to ​IMPLementation）是C++中实现接口与实现分离的核心技术，通过隐藏实现细节显著提升代码的封装性、编译效率和二进制兼容性。




#### 6.dynamic_cast
C++中唯一具有运行时类型检查能力的类型转换操作符，主要用于多态的安全转换。
