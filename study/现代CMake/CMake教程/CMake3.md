[TOC]



## 
![alt text](image.png)

### 为什么学现代CMake？

![alt text](image-1.png)

![alt text](image-2.png)


### 命令行
![alt text](image-3.png)

#### -B 构建cmake

![alt text](image-4.png)

#### -D 配置变量
![alt text](image-13.png)

#### -G 生成器Ninga
![alt text](image-14.png)
![alt text](image-15.png)



### 添加源文件

#### 一个源文件
![alt text](image-5.png)
![alt text](image-6.png)

#### 多个源文件
![alt text](image-7.png)

![alt text](image-8.png)

#### 源码在子文件夹 建议都放到src下
![alt text](image-9.png)

![alt text](image-10.png)

![alt text](image-11.png)
![alt text](image-12.png)

---
### 项目配置变量

#### CMAKE_BUILD_TYPE 调试发布
![alt text](image-16.png)
![alt text](image-17.png)
![alt text](image-18.png)

#### project: 初始化项目信息

https://cmake.org/cmake/help/latest/command/project.html


![alt text](image-19.png)

![alt text](image-20.png)
![alt text](image-21.png)
![alt text](image-22.png)
![alt text](image-23.png)

#### project: LANGUAGES
![alt text](image-24.png)

![alt text](image-25.png)

![alt text](image-26.png)

#### project: VERSION
显示版本号
![alt text](image-30.png)

#### project: 一些描述
![alt text](image-31.png)
![alt text](image-32.png)

#### C++标准： CMAKE_CXX_STANDARD

https://crascit.com/2015/03/28/enabling-cxx11-in-cmake/

![alt text](image-27.png)

![alt text](image-28.png)

![alt text](image-29.png)

#### CMAKE的 ${} 表达式
![alt text](image-33.png)


#### CMAKE cmake_minimum_required 指定最低版本
https://runebook.dev/zh-CN/docs/cmake/command/cmake_minimum_required#policy-settings

![alt text](image-34.png)
![alt text](image-35.png)

![alt text](image-38.png)


#### cmake --version
![alt text](image-36.png)

#### cmake 更新
![alt text](image-37.png)

#### tools
![alt text](image-39.png)

#### 一个CMakeLists.txt 标准模板
![alt text](image-40.png)


### 链接库文件

#### add_executable
![alt text](image-41.png)


#### target_link_libraries
![alt text](image-42.png)

#### add_library

![alt text](image-44.png)

![alt text](image-49.png)


#### 对象库 OBJECT
https://www.scivision.dev/cmake-object-libraries/

![alt text](image-45.png)

![alt text](image-47.png)

#### 静态库

![alt text](image-46.png)

#### 动态库
![alt text](image-48.png)


#### BUILD_SHARED_LIBS
![alt text](image-50.png)

![alt text](image-51.png)

#### 常见坑点：动态库无法链接静态库
![alt text](image-52.png)

动态库 ：内存中的地址会变化 指定PIC
静态库 ： 地址不变换 没指定

![alt text](image-53.png)
![alt text](image-54.png)


---
### 对象的属性

#### set_property
![alt text](image-55.png)

#### set_target_properties
![alt text](image-56.png)

#### set
![alt text](image-57.png)


#### 错误示例
![alt text](image-58.png)

#### windows 动态链接库
![alt text](image-59.png)

![alt text](image-60.png)

![alt text](image-61.png)

##### 解决
![alt text](image-62.png)

![alt text](image-63.png)

![alt text](image-64.png)


---

### 连接第三方库

#### 案例 TBB
![alt text](image-65.png)

![alt text](image-66.png)

![alt text](image-67.png)

#### find_package ——QT
![alt text](image-68.png)

![alt text](image-69.png)

![alt text](image-71.png)

![alt text](image-72.png)

![alt text](image-74.png)

![alt text](image-80.png)

![alt text](image-81.png)

![alt text](image-82.png)

#### QT

![alt text](image-75.png)

![alt text](image-76.png)

![alt text](image-77.png)

![alt text](image-78.png)

![alt text](image-79.png)


#### PUBLIC
![alt text](image-70.png)



#### 老年案例
![alt text](image-73.png)



### 输出与变量

#### message
![alt text](image-83.png)

![alt text](image-84.png)

![alt text](image-85.png)

![alt text](image-86.png)

![alt text](image-87.png)

![alt text](image-88.png)

![alt text](image-89.png)

![alt text](image-90.png)

![alt text](image-91.png)

![alt text](image-92.png)

### 变量和缓存

#### 缓存

##### 重复执行 cmake -B build 
![alt text](image-93.png)

##### 清除缓存
![alt text](image-94.png)

![alt text](image-95.png)

![alt text](image-96.png)

##### find_package缓存机制
![alt text](image-97.png)

##### 设置缓存变量set
![alt text](image-98.png)

![alt text](image-99.png)

##### 常见问题
![alt text](image-100.png)

##### 更新缓存 删build
![alt text](image-101.png)

![alt text](image-102.png)

![alt text](image-103.png)

![alt text](image-104.png)

![alt text](image-105.png)

https://www.cnblogs.com/Braveliu/p/15614013.html


#### 案例
![alt text](image-106.png)

![alt text](image-107.png)

![alt text](image-108.png)

已经进缓存了
![alt text](image-109.png)

![alt text](image-110.png)

![alt text](image-111.png)

option ccmake可以看到
![alt text](image-112.png)

### 跨平台与编辑器

#### Cmake中定义宏

#### target_compile_definitions
![alt text](image-113.png)

![alt text](image-114.png)

![alt text](image-115.png)

#### 生成器表达式
https://cmake.org/cmake/help/latest/manual/cmake-generator-expressions.7.html#genex:PLATFORM_ID

![alt text](image-116.png)

![alt text](image-117.png)

https://cmake.org/cmake/help/latest/variable/CMAKE_LANG_COMPILER_ID.html#variable:CMAKE_%3CLANG%3E_COMPILER_ID


![alt text](image-118.png)

![alt text](image-119.png)


![alt text](image-120.png)


![alt text](image-121.png)

![alt text](image-122.png)

#### 指定编辑器

![alt text](image-123.png)

![alt text](image-124.png)


![alt text](image-125.png)


#### vimrc
如何安装插件
github.com/archibate/vimrc

![alt text](image-126.png)


### 分支与判断

#### BOOL
![alt text](image-127.png)

#### if
![alt text](image-128.png)

![alt text](image-129.png)

![alt text](image-130.png)

![alt text](image-131.png)

### 变量与作用域

#### 父子模块变量传播
![alt text](image-132.png)
![alt text](image-133.png)

![alt text](image-134.png)

![alt text](image-135.png)

![alt text](image-136.png)

#### 独立作用域
![alt text](image-137.png)

#### 环境变量 访问
![alt text](image-138.png)

![alt text](image-139.png)


#### 缓存变量 访问
![alt text](image-140.png)

#### ${} 找局部变量 | 缓存变量
![alt text](image-141.png)

#### if (DEFINED)
![alt text](image-142.png)

![alt text](image-143.png)

![alt text](image-144.png)

#### if (DEFINED ENV{xx})
![alt text](image-145.png)

#### bash设置环境变量尝试
![alt text](image-146.png)

![alt text](image-147.png)

export X=1
echo $X
/
X=3 env

#### 其他建议

##### CCache
![alt text](image-148.png)

##### run伪目标
![alt text](image-149.png)


##### configure伪目标
![alt text](image-150.png)

### 其他
![alt text](image-151.png)
