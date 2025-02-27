[TOC]

### 整体结构

![alt text](image.png)

![alt text](image-1.png)
> 局部变量放入栈中，由编译器和操作系统决定它的生命周期
> 程序员 new一个变量或者自己分配的内存放入堆

![alt text](image-2.png)

### 内存结构详解
#### 代码区
![alt text](image-3.png)
![alt text](image-4.png)
> 4、5指令放到代码段中，“”数据放入只读数据段中。

![alt text](image-5.png)
![alt text](image-6.png)
![alt text](image-7.png)
> 函数的代码段地址与 压栈出栈有关

![alt text](image-8.png)
![alt text](image-10.png)

#### 常量存储区
![alt text](image-11.png)
![alt text](image-13.png)
![alt text](image-12.png)

#### 全局/静态存储区
![alt text](image-14.png)
![alt text](image-15.png)
![alt text](image-16.png)
![alt text](image-17.png)
![alt text](image-18.png)

#### 栈
![alt text](image-19.png)
![alt text](image-22.png)
![alt text](image-20.png)
![alt text](image-21.png)
![alt text](image-23.png)
![alt text](image-24.png)

#### 堆
![alt text](image-25.png)
![alt text](image-26.png)
![alt text](image-28.png)
![alt text](image-29.png)
![alt text](image-30.png)

#### 小结
![alt text](image-31.png)
![alt text](image-32.png)
> 内存泄漏new delete
> 野指针 初始化
> 栈溢出 陷于死循环 大量局部变量压栈
> 悬空指针 指针指向的内存被释放了但指针还未被删除
> 智能指针 本质封装了一个原始C++指针的类模板，释放原理是依靠类对象的析构函数实现的
>
![alt text](image-33.png)
![alt text](image-34.png)
![alt text](image-35.png)