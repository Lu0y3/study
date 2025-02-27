[TOC]

### 重要概念
![alt text](image-1.png)
![alt text](image.png)

### 文件的打开和关闭
![alt text](image-2.png)
![alt text](image-3.png)
![alt text](image-4.png)
![alt text](image-5.png)
![alt text](image-6.png)
![alt text](image-7.png)

### 写文件

![alt text](image-8.png)


### 读文件
![alt text](image-9.png)
![alt text](image-10.png)
![alt text](image-11.png)
![alt text](image-12.png)
解决汉字乱码
![alt text](image-13.png)
![alt text](image-14.png) >>不读空格 回车
![alt text](image-15.png) get()读空格和回车

---
![alt text](image-16.png)
> **代码中存在错误，附加修改和扩展**

![alt text](image-17.png)
![alt text](image-19.png)
![alt text](image-18.png)

> fstream.seekg(0,ios::end);`seekg`是C++中用于移动输入文件流指针的函数，参数`0`表示偏移量，`ios::end`表示相对于文件末尾的位置。
> 
> `tellg()`用于获取当前输入文件流指针的位置，返回类型是`streampos`。
> ![alt text](image-20.png)
>![alt text](image-21.png)
> seekg(0, ios::end) 将指针移动到文件末尾
> tellg() 返回当前指针位置（即总字节数）
>

![alt text](image-22.png)
```C++
#include <iostream>
#include <fstream>
using namespace std;

int main() {
    const int bufferSize = 100;
    char buffer[bufferSize];

    ifstream inputFile("data.bin", ios::binary);
    if (!inputFile) {
        cerr << "文件打开失败" << endl;
        return 1;
    }

    // 逐块读取文件
    while (inputFile.read(buffer, bufferSize)) {
        // 处理当前读取的数据块
        streamsize bytesRead = inputFile.gcount();  // ✅ 正确函数名
        for (int i = 0; i < bytesRead; ++i) {
            // 正确处理符号问题
            cout << hex << static_cast<int>(static_cast<unsigned char>(buffer[i])) << " ";
        }
    }

    // 处理最后一次可能未填满缓冲区的读取
    if (inputFile.eof()) {
        streamsize bytesRead = inputFile.gcount();
        for (int i = 0; i < bytesRead; ++i) {
            cout << hex << static_cast<int>(static_cast<unsigned char>(buffer[i])) << " ";
        }
    } else if (inputFile.fail()) {
        cerr << "读取过程中发生错误" << endl;
    }

    inputFile.close();
    return 0;
}
```
![alt text](image-25.png)
![alt text](image-24.png)
![alt text](image-23.png)

#### 异常处理
![alt text](image-26.png)
![alt text](image-28.png)
![alt text](image-27.png)

#### 成员函数
![alt text](image-29.png)
![alt text](image-30.png)
![alt text](image-31.png)

![alt text](image-32.png)
![alt text](image-33.png)

### 文件指针和定位 
指针-> 光标
![alt text](image-34.png)
![alt text](image-35.png)
![alt text](image-36.png)
![alt text](image-37.png)
![alt text](image-44.png)

![alt text](image-43.png)
![alt text](image-41.png)
> seekp的实现会产生覆盖，，我们可以使用拼接的方式插入
>

![alt text](image-39.png)
![alt text](image-40.png)

### 应用案例
![alt text](image-45.png)
