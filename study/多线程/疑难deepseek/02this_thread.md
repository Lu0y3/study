
# `std::this_thread` 详解

## 一、核心功能概览
该命名空间提供操作**当前线程**的实用函数，需包含头文件 `<thread>`

| 函数                     | 作用                          |
|--------------------------|-------------------------------|
| `get_id()`               | 获取当前线程的唯一标识符      |
| `yield()`                | 主动让出CPU时间片             |
| `sleep_for(duration)`    | 阻塞当前线程指定时间段        |
| `sleep_until(time_point)`| 阻塞到指定时间点              |

---

## 二、函数详解与代码示例

### 1. `get_id()`：获取线程ID
```cpp
#include <iostream>
#include <thread>

void print_thread_id() {
    std::cout << "Current thread ID: " 
              << std::this_thread::get_id() 
              << std::endl;
}

int main() {
    std::thread t1(print_thread_id);
    print_thread_id();  // 主线程ID
    t1.join();
    return 0;
}
```
**输出示例**：
```
Current thread ID: 140245867429696  // 主线程
Current thread ID: 140245859036928  // t1线程
```

---

### 2. `yield()`：主动让出CPU
**适用场景**：忙等待优化（替代自旋锁）
```cpp
#include <atomic>
std::atomic<bool> ready(false);

void consumer() {
    while (!ready) {
        std::this_thread::yield(); // 让出CPU，避免忙等待
    }
    std::cout << "Data ready!" << std::endl;
}

void producer() {
    // 模拟耗时操作
    std::this_thread::sleep_for(std::chrono::seconds(1));
    ready = true;
}

int main() {
    std::thread t1(consumer);
    std::thread t2(producer);
    t1.join();
    t2.join();
}
```

---

### 3. `sleep_for()`：定时阻塞
```cpp
#include <chrono>

void timed_task() {
    std::cout << "Task start" << std::endl;
    // 阻塞当前线程3秒
    std::this_thread::sleep_for(std::chrono::seconds(3));
    std::cout << "Task end" << std::endl;
}

int main() {
    std::thread t(timed_task);
    t.join();
    return 0;
}
```

---

### 4. `sleep_until()`：阻塞到指定时间点
```cpp
void alarm_clock() {
    auto now = std::chrono::system_clock::now();
    auto alarm_time = now + std::chrono::hours(1); // 1小时后触发

    std::this_thread::sleep_until(alarm_time);
    std::cout << "Wake up!" << std::endl;
}
```

---

## 三、关键应用场景

### 1. 性能优化
• 在自旋锁场景中使用 `yield()` 减少CPU空转消耗
• 替代简单的忙等待循环：
  ```cpp
  // 不良实践（高CPU占用）
  while (!condition) {}

  // 改进方案
  while (!condition) {
      std::this_thread::yield();
  }
  ```

### 2. 定时任务调度
```cpp
// 每5秒执行一次任务
void periodic_task() {
    while (true) {
        auto next_run = std::chrono::steady_clock::now() 
                      + std::chrono::seconds(5);
        perform_task();
        std::this_thread::sleep_until(next_run);
    }
}
```

### 3. 调试辅助
```cpp
// 测量代码执行时间
auto start = std::chrono::high_resolution_clock::now();
critical_operation();
auto end = std::chrono::high_resolution_clock::now();
std::cout << "Cost: " 
          << std::chrono::duration_cast<std::chrono::milliseconds>(end - start).count()
          << "ms" << std::endl;
```

---

## 四、注意事项
1. **时间精度问题**：
   • 实际休眠时间可能长于指定时间（受系统调度影响）
   • 精度依赖操作系统，通常为毫秒级

2. **跨平台行为差异**：
   • Windows最小休眠间隔约15ms
   • Linux实时系统可达到微秒级精度

3. **资源管理**：
   • 避免在持有锁的情况下长时间休眠
   • 结合条件变量实现高效等待：
     ```cpp
     std::mutex mtx;
     std::condition_variable cv;
     // 更高效的等待方式
     std::unique_lock<std::mutex> lock(mtx);
     cv.wait_for(lock, std::chrono::seconds(2));
     ```

---

**最佳实践建议**：优先使用 `sleep_for`/`sleep_until` 代替忙等待，合理使用 `yield` 优化CPU占用，通过 `get_id` 实现多线程调试日志。