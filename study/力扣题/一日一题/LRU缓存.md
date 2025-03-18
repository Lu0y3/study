https://leetcode.cn/problems/lru-cache



```cpp
#include <unordered_map>
using namespace std;

// 双向链表节点结构体定义[1,3](@ref)
struct Node {
    int key, val;       // 存储键值对
    Node *prev, *next;   // 前驱/后继指针
    Node(int k, int v) : key(k), val(v), prev(nullptr), next(nullptr) {}
};

class LRUCache {
private:
    int cap;             // 缓存容量
    Node *head, *tail;   // 哑头尾节点（哨兵节点）[3,5](@ref)
    unordered_map<int, Node*> cache;  // 哈希表实现O(1)查找[2,6](@ref)

    // 添加节点到链表头部（最近访问位置）
    void addNode(Node* node) {
        node->prev = head;         // 新节点前驱指向头哨兵
        node->next = head->next;   // 新节点后继指向原头节点
        head->next->prev = node;   // 原头节点前驱指向新节点
        head->next = node;         // 头哨兵后继指向新节点
    }

    // 移除指定节点（用于访问时的位置调整）
    void removeNode(Node* node) {
        node->prev->next = node->next;  // 前驱节点跳过当前节点
        node->next->prev = node->prev;  // 后继节点连接前驱节点
    }

    // 将节点移动到链表头部（标记为最近使用）
    void moveToHead(Node* node) {
        removeNode(node);  // 先从当前位置移除
        addNode(node);     // 再插入头部
    }

public:
    // 构造函数初始化哨兵节点[3](@ref)
    LRUCache(int capacity) : cap(capacity) {
        head = new Node(-1, -1);  // 创建头哨兵
        tail = new Node(-1, -1);  // 创建尾哨兵
        head->next = tail;        // 初始化空链表
        tail->prev = head;
    }

    // 查询操作：时间复杂度O(1)
    int get(int key) {
        if (cache.find(key) == cache.end()) 
            return -1;            // 未找到返回-1[4](@ref)
        
        Node* node = cache[key];
        moveToHead(node);         // 更新为最近使用[5](@ref)
        return node->val;
    }

    // 插入/更新操作：时间复杂度O(1)
    void put(int key, int value) {
        if (cache.find(key) != cache.end()) {  // 已存在键
            Node* node = cache[key];
            node->val = value;    // 更新值[1](@ref)
            moveToHead(node);     // 提升为最近使用
        } else {                  // 新增键
            Node* newNode = new Node(key, value);
            cache[key] = newNode; // 存入哈希表
            addNode(newNode);      // 插入链表头部
            
            if (cache.size() > cap) {  // 容量超额处理
                Node* lru = tail->prev; // 获取LRU节点[6](@ref)
                removeNode(lru);       // 从链表移除
                cache.erase(lru->key); // 从哈希表删除
                delete lru;            // 释放内存（实际工程建议用智能指针）[2](@ref)
            }
        }
    }
};

/**
 * 使用示例：
 * LRUCache* obj = new LRUCache(capacity);
 * int param_1 = obj->get(key);
 * obj->put(key,value);
 */
```