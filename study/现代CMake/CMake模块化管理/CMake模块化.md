## C/C++ 项目


### 文件/目录组织规范化
![alt text](image.png)

#### 目录组织方式

![alt text](image-2.png)
![alt text](image-3.png)


https://github.com/parallel101/course/tree/master/16/00

防止和系统内部的混淆
![alt text](image-1.png)


##### 划分子项目
![alt text](image-4.png)

库文件：作代码逻辑

可执行文件 ： 与用户交互的逻辑

![alt text](image-6.png)


##### 根项目的 CMakeLists.txt 配置
![alt text](image-5.png)


##### 子项目的 CMakeLists.txt 配置
![alt text](image-7.png)

##### 子项目的头文件
![alt text](image-8.png)

##### 子项目的源文件
![alt text](image-9.png)

##### file GLOB
![alt text](image-10.png)

##### 头文件与源文件一一对应
![alt text](image-11.png)

##### 没有源文件只有头文件
![alt text](image-12.png)

static 是内部链接
inline 是外部链接

##### 每添加一个功能，创建两个文件
![alt text](image-13.png)

##### 一个模块依赖另一个模块，应引入它的头文件
![alt text](image-14.png)

##### 依赖其他模块但不解引用，则可以只前向声明不导入头文件
![alt text](image-15.png)

##### 以项目名为名字空间（namsepace），避免符号冲突
![alt text](image-16.png)

类的属性都是inline属性的，比全局属性还要危险


##### 依赖另一个子项目，则需要链接他
![alt text](image-17.png)

##### include"" 和 <>
![alt text](image-18.png)

##### 你知道吗？CMake 也有 include 功能
![alt text](image-19.png)


**通常把一些脚本文件放到cmake子目录里**
![alt text](image-20.png)

---
##### macro 和 function 的区别

https://cmake.org/cmake/help/latest/command/function.html
https://cmake.org/cmake/help/latest/command/macro.html

![alt text](image-21.png)

---
##### include 和 add_subdirectory 的区别
![alt text](image-22.png)

---
### 第三方库/依赖项配置

![alt text](image-23.png)
#### find_package

##### find_package 命令
https://cmake.org/cmake/help/latest/command/find_package.html

![alt text](image-24.png)

![alt text](image-25.png)

##### find_package 找"包"实际上是找什么
![alt text](image-26.png)


![alt text](image-27.png)

##### 搜索路径

![alt text](image-28.png)

![alt text](image-29.png)

![alt text](image-30.png)

![alt text](image-31.png)

#### 安装在非标准路径库
![alt text](image-32.png)

##### 举例 windows\linux qt
![alt text](image-33.png)

![alt text](image-34.png)

![alt text](image-35.png)

#### 科普
##### 科普：类似 Qt 这种亲 Unix 软件

![alt text](image-36.png)

![alt text](image-37.png)

##### 科普：亲 Unix 软件从源码安装的通用套路
![alt text](image-38.png)


#### 如果第三方库发懒，没有提供 Config 文件怎么办？
![alt text](image-39.png)

![alt text](image-40.png)


##### 举例：FindJemalloc.cmake

![alt text](image-42.png)

![alt text](image-43.png)
![alt text](image-41.png)
https://github.com/AcademySoftwareFoundation/openvdb/blob/master/cmake/FindJemalloc.cmake

#### 现代 vs 古代

##### 现代 vs 古代：用法上完全不同！
![alt text](image-44.png)

**具体还是要看包的源码**

---
##### 现代和古代的区别
![alt text](image-45.png)
![alt text](image-46.png)

##### 兼容
![alt text](image-47.png)

---

### find_package两种模式
![alt text](image-48.png)
![alt text](image-49.png)


### 关于 vcpkg 的坑（不用 vcpkg 的同学可以跳过这段）
![alt text](image-50.png)

### 科普：语义版本号（semantic versioning）系统
![alt text](image-51.png)
https://cmake.org/cmake/help/latest/command/if.html

### find_package 命令指定版本

![alt text](image-52.png)

### 总结
![alt text](image-53.png)

![alt text](image-54.png)

### 古代 CMake 常见问题

![alt text](image-55.png)
![alt text](image-56.png)


### 少见的 add_subdirectory 邪教

![alt text](image-57.png)


## 科普 ：怎么安装库
### osg
MacOS ?

![alt text](image-58.png)
![alt text](image-59.png)
![alt text](image-60.png)


![alt text](image-62.png)

**C++**
![alt text](image-61.png)

![alt text](image-63.png)
![alt text](image-64.png)

![alt text](image-65.png)

![alt text](image-66.png)

![alt text](image-67.png)

![alt text](image-68.png)



### physX
英伟达 不开源！

### tbb cuda

![alt text](image-69.png)

![alt text](image-70.png)

![alt text](image-71.png)

![alt text](image-72.png)
![alt text](image-73.png)

![alt text](image-74.png)

![alt text](image-75.png)
![alt text](image-76.png)


---


