以下是 **线程安全的 `SharedPtr` 完整实现**，包含详细的代码注释和全面的测试用例，覆盖单线程、多线程场景及边界条件。

---

### **一、SharedPtr 源码（线程安全版）**

```cpp
#include <atomic>    // std::atomic
#include <utility>   // std::swap
#include <iostream>  // 测试用

template <typename T>
class SharedPtr {
private:
    T* ptr_ = nullptr;
    std::atomic<size_t>* ref_count_ = nullptr;  // 原子引用计数器

    // 释放资源（原子操作）
    void release() noexcept {
        if (ref_count_) {
            // 原子递减，获取递减后的值
            size_t remaining = ref_count_->fetch_sub(1, std::memory_order_acq_rel);
            if (remaining == 1) {  // 最后一个持有者
                delete ptr_;
                delete ref_count_;
            }
            ptr_ = nullptr;
            ref_count_ = nullptr;
        }
    }

public:
    // ------------------- 构造函数与析构函数 -------------------
    // 默认构造（空指针）
    SharedPtr() = default;

    // 显式构造函数（接管原始指针）
    explicit SharedPtr(T* ptr) : ptr_(ptr), ref_count_(new std::atomic<size_t>(1)) {}

    // 拷贝构造函数（共享所有权，原子递增）
    SharedPtr(const SharedPtr& other) noexcept : ptr_(other.ptr_), ref_count_(other.ref_count_) {
        if (ref_count_) {
            ref_count_->fetch_add(1, std::memory_order_relaxed);
        }
    }

    // 移动构造函数（转移所有权）
    SharedPtr(SharedPtr&& other) noexcept : ptr_(other.ptr_), ref_count_(other.ref_count_) {
        other.ptr_ = nullptr;
        other.ref_count_ = nullptr;
    }

    // 析构函数
    ~SharedPtr() {
        release();
    }

    // ------------------- 赋值运算符 -------------------
    // 拷贝赋值（原子操作）
    SharedPtr& operator=(const SharedPtr& other) noexcept {
        if (this != &other) {
            release();  // 释放当前资源
            ptr_ = other.ptr_;
            ref_count_ = other.ref_count_;
            if (ref_count_) {
                ref_count_->fetch_add(1, std::memory_order_relaxed);
            }
        }
        return *this;
    }

    // 移动赋值
    SharedPtr& operator=(SharedPtr&& other) noexcept {
        if (this != &other) {
            release();
            ptr_ = other.ptr_;
            ref_count_ = other.ref_count_;
            other.ptr_ = nullptr;
            other.ref_count_ = nullptr;
        }
        return *this;
    }

    // ------------------- 成员函数 -------------------
    // 解引用操作符
    T& operator*() const noexcept {
        return *ptr_;
    }

    // 箭头操作符
    T* operator->() const noexcept {
        return ptr_;
    }

    // 获取原始指针
    T* get() const noexcept {
        return ptr_;
    }

    // 获取引用计数
    size_t use_count() const noexcept {
        return (ref_count_ ? ref_count_->load(std::memory_order_relaxed) : 0);
    }

    // 重置指针
    void reset(T* ptr = nullptr) {
        release();  // 释放当前资源
        if (ptr) {
            ptr_ = ptr;
            ref_count_ = new std::atomic<size_t>(1);
        }
    }

    // 交换指针
    void swap(SharedPtr& other) noexcept {
        std::swap(ptr_, other.ptr_);
        std::swap(ref_count_, other.ref_count_);
    }

    // 显式布尔转换（判空）
    explicit operator bool() const noexcept {
        return ptr_ != nullptr;
    }

    // 释放所有权（不释放资源）
    T* release() noexcept {
        T* raw_ptr = ptr_;
        ptr_ = nullptr;
        ref_count_ = nullptr;  // 注意：此处不修改引用计数！
        return raw_ptr;
    }
};
```

---

### **二、完整测试用例**

```cpp
#include <cassert>
#include <thread>
#include <vector>

// 测试辅助类：统计析构次数
class TestObject {
public:
    static std::atomic<int> destruct_count;
    TestObject() = default;
    ~TestObject() {
        destruct_count.fetch_add(1, std::atomic::memory_order_relaxed);
    }
};
std::atomic<int> TestObject::destruct_count{0};

// ------------------- 测试用例 -------------------
// 测试用例 1：基础构造与析构
void test_constructor_and_destructor() {
    TestObject::destruct_count = 0;
    {
        SharedPtr<TestObject> p1(new TestObject);
        assert(p1.use_count() == 1);

        SharedPtr<TestObject> p2 = p1;  // 拷贝构造
        assert(p1.use_count() == 2);
        assert(p2.use_count() == 2);
    }  // p1 和 p2 析构
    assert(TestObject::destruct_count == 1);
}

// 测试用例 2：移动语义
void test_move_semantics() {
    TestObject::destruct_count = 0;
    {
        SharedPtr<TestObject> p1(new TestObject);
        SharedPtr<TestObject> p2 = std::move(p1);  // 移动构造

        assert(p1.get() == nullptr);
        assert(p2.use_count() == 1);

        SharedPtr<TestObject> p3;
        p3 = std::move(p2);  // 移动赋值
        assert(p2.get() == nullptr);
        assert(p3.use_count() == 1);
    }
    assert(TestObject::destruct_count == 1);
}

// 测试用例 3：reset 和 release
void test_reset_and_release() {
    TestObject::destruct_count = 0;
    {
        SharedPtr<TestObject> p1(new TestObject);
        p1.reset();  // 重置为空
        assert(p1.use_count() == 0);

        p1.reset(new TestObject);  // 重置为新对象
        assert(p1.use_count() == 1);

        TestObject* raw_ptr = p1.release();  // 释放所有权
        assert(p1.use_count() == 0);
        delete raw_ptr;  // 手动释放
    }
    assert(TestObject::destruct_count == 1);
}

// 测试用例 4：自我赋值和 swap
void test_self_assignment_and_swap() {
    TestObject::destruct_count = 0;
    {
        SharedPtr<TestObject> p1(new TestObject);
        SharedPtr<TestObject> p2 = p1;

        // 自我赋值
        p1 = p1;  // 应该无操作
        assert(p1.use_count() == 2);

        // 交换
        p1.swap(p2);
        assert(p1.use_count() == 2);
        assert(p2.use_count() == 2);
    }
    assert(TestObject::destruct_count == 1);
}

// 测试用例 5：多线程安全
void test_thread_safety() {
    TestObject::destruct_count = 0;
    constexpr int kThreadCount = 100;    // 线程数
    constexpr int kLoopPerThread = 1000; // 每个线程循环次数

    SharedPtr<TestObject> global_ptr(new TestObject);
    std::vector<std::thread> threads;

    // 创建线程：反复拷贝和释放指针
    for (int i = 0; i < kThreadCount; ++i) {
        threads.emplace_back([&global_ptr] {
            for (int j = 0; j < kLoopPerThread; ++j) {
                SharedPtr<TestObject> local_ptr = global_ptr;  // 原子递增
                assert(local_ptr.get() != nullptr);
                local_ptr.reset();  // 原子递减
            }
        });
    }

    // 等待所有线程结束
    for (auto& t : threads) {
        t.join();
    }

    // 全局指针的引用计数应恢复为 1
    assert(global_ptr.use_count() == 1);
    global_ptr.reset();  // 显式释放
    assert(TestObject::destruct_count == 1);
}

// 主函数
int main() {
    test_constructor_and_destructor();
    std::cout << "Test 1 passed." << std::endl;

    test_move_semantics();
    std::cout << "Test 2 passed." << std::endl;

    test_reset_and_release();
    std::cout << "Test 3 passed." << std::endl;

    test_self_assignment_and_swap();
    std::cout << "Test 4 passed." << std::endl;

    test_thread_safety();
    std::cout << "Test 5 passed." << std::endl;

    std::cout << "All tests passed!" << std::endl;
    return 0;
}
```

---

### **三、编译与运行**

#### **1. 编译命令**
```bash
g++ -std=c++11 -pthread -o shared_ptr_test shared_ptr.cpp && ./shared_ptr_test
```

#### **2. 预期输出**
```
Test 1 passed.
Test 2 passed.
Test 3 passed.
Test 4 passed.
Test 5 passed.
All tests passed!
```

---

### **四、关键测试点说明**

| **测试用例**              | **验证内容**                                                                 |
|---------------------------|-----------------------------------------------------------------------------|
| `test_constructor_and_destructor` | 构造、拷贝、析构的正确性，引用计数准确性                                      |
| `test_move_semantics`      | 移动构造和移动赋值后原指针置空，资源无重复释放                                |
| `test_reset_and_release`   | `reset()` 释放资源，`release()` 放弃所有权                                   |
| `test_self_assignment_and_swap` | 自我赋值不改变引用计数，`swap()` 正确交换指针和计数器                         |
| `test_thread_safety`       | 多线程环境下引用计数的原子性，资源仅释放一次                                  |

---

### **五、扩展建议**

1. **自定义删除器**  
   修改 `SharedPtr` 模板，支持传入自定义删除器（如 `Deleter`），以管理文件句柄、网络连接等资源。

2. **弱引用 (`WeakPtr`)**  
   实现 `WeakPtr` 类解决循环引用问题，弱引用不增加引用计数。

3. **内存优化**  
   模仿 `std::make_shared`，将对象和控制块内存合并分配，减少内存碎片。

通过此实现和测试，可深入理解智能指针的线程安全机制及 C++ 资源管理核心思想。