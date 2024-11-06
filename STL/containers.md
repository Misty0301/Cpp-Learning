# 容器

## Sequence Containers 顺序容器
1. vector
    动态数组，支持快速随机访问，插入删除元素效率高，适用于频繁访问的场景。
    以下是 `std::vector` 在 C++ 中的所有常用接口及其详细描述。包括构造函数、容量管理、元素访问、修改操作、分配器、迭代器以及其他辅助函数等内容。
### 1. **构造函数**
- **默认构造函数**：
  ```cpp
  std::vector<T> vec;
  ```
  创建一个空的 `vector`。

- **指定大小的构造函数**：
  ```cpp
  std::vector<T> vec(size_t count);
  ```
  创建一个包含 `count` 个元素的 `vector`，每个元素的值为默认值。

- **指定大小和初始值的构造函数**：
  ```cpp
  std::vector<T> vec(size_t count, const T& value);
  ```
  创建一个包含 `count` 个元素的 `vector`，每个元素的值为 `value`。

- **使用迭代器的构造函数**：
  ```cpp
  template<class InputIterator>
  std::vector<T> vec(InputIterator first, InputIterator last);
  ```
  创建一个 `vector`，包含 `[first, last)` 范围内的元素。

- **拷贝构造函数**：
  ```cpp
  std::vector<T> vec(const std::vector<T>& other);
  ```
  创建一个新的 `vector`，内容为 `other` 的拷贝。

- **移动构造函数**（C++11 引入）：
  ```cpp
  std::vector<T> vec(std::vector<T>&& other);
  ```
  移动构造 `other` 的内容到新 `vector`，`other` 将变为空。

### 2. **容量管理函数**
- **`size()`**：
  ```cpp
  size_t size() const noexcept;
  ```
  返回 `vector` 中的元素个数。

- **`capacity()`**：
  ```cpp
  size_t capacity() const noexcept;
  ```
  返回 `vector` 的容量（已分配但未使用的存储空间数量）。

- **`resize()`**：
  ```cpp
  void resize(size_t count);
  void resize(size_t count, const T& value);
  ```
  调整 `vector` 的大小为 `count`，如果增大，新元素初始化为默认值或指定的 `value`。

- **`reserve()`**：
  ```cpp
  void reserve(size_t new_cap);
  ```
  预留存储空间，使 `vector` 的容量至少为 `new_cap`，减少动态分配次数。

- **`shrink_to_fit()`**（C++11 引入）：
  ```cpp
  void shrink_to_fit();
  ```
  请求 `vector` 释放未使用的内存，减少容量到等于当前大小。

- **`empty()`**：
  ```cpp
  bool empty() const noexcept;
  ```
  判断 `vector` 是否为空（即 `size() == 0`）。

### 3. **元素访问函数**
- **`operator[]`**：
  ```cpp
  T& operator[](size_t pos);
  const T& operator[](size_t pos) const;
  ```
  返回指定位置 `pos` 处的元素，注意没有边界检查。

- **`at()`**：
  ```cpp
  T& at(size_t pos);
  const T& at(size_t pos) const;
  ```
  返回指定位置 `pos` 处的元素，带有边界检查，超出范围会抛出 `std::out_of_range` 异常。

- **`front()`**：
  ```cpp
  T& front();
  const T& front() const;
  ```
  返回第一个元素的引用。

- **`back()`**：
  ```cpp
  T& back();
  const T& back() const;
  ```
  返回最后一个元素的引用。

- **`data()`**：
  ```cpp
  T* data() noexcept;
  const T* data() const noexcept;
  ```
  返回指向内部数组首元素的指针，用于与 C 风格数组的兼容操作。

### 4. **修改函数**
- **`push_back()`**：
  ```cpp
  void push_back(const T& value);
  void push_back(T&& value);
  ```
  在 `vector` 的末尾添加一个元素。

- **`pop_back()`**：
  ```cpp
  void pop_back();
  ```
  移除 `vector` 末尾的元素。

- **`insert()`**：
  ```cpp
  iterator insert(const_iterator pos, const T& value);
  iterator insert(const_iterator pos, T&& value);
  iterator insert(const_iterator pos, size_t count, const T& value);
  template<class InputIt>
  iterator insert(const_iterator pos, InputIt first, InputIt last);
  ```
  在指定位置 `pos` 插入元素或范围，返回指向新插入元素的迭代器。

- **`erase()`**：
  ```cpp
  iterator erase(const_iterator pos);
  iterator erase(const_iterator first, const_iterator last);
  ```
  移除指定位置或范围内的元素，返回指向移除后下一个元素的迭代器。

- **`clear()`**：
  ```cpp
  void clear() noexcept;
  ```
  清空 `vector` 中的所有元素。

- **`emplace()`**（C++11 引入）：
  ```cpp
  template<class... Args>
  iterator emplace(const_iterator pos, Args&&... args);
  ```
  在指定位置 `pos` 处直接构造元素。

- **`emplace_back()`**（C++11 引入）：
  ```cpp
  template<class... Args>
  void emplace_back(Args&&... args);
  ```
  在 `vector` 的末尾直接构造元素。

- **`assign()`**：
  ```cpp
  void assign(size_t count, const T& value);
  template<class InputIt>
  void assign(InputIt first, InputIt last);
  ```
  用指定个数的值或者范围来替换 `vector` 的内容。

- **`swap()`**：
  ```cpp
  void swap(vector& other) noexcept;
  ```
  交换两个 `vector` 的内容。

### 5. **分配器函数**
- **`get_allocator()`**：
  ```cpp
  allocator_type get_allocator() const noexcept;
  ```
  返回 `vector` 使用的分配器对象。

### 6. **迭代器函数**
- **`begin()` 和 `end()`**：
  ```cpp
  iterator begin() noexcept;
  const_iterator begin() const noexcept;
  iterator end() noexcept;
  const_iterator end() const noexcept;
  ```
  返回指向 `vector` 起始位置和结束位置的迭代器。

- **`rbegin()` 和 `rend()`**：
  ```cpp
  reverse_iterator rbegin() noexcept;
  const_reverse_iterator rbegin() const noexcept;
  reverse_iterator rend() noexcept;
  const_reverse_iterator rend() const noexcept;
  ```
  返回指向 `vector` 末尾的反向迭代器。

- **`cbegin()`、`cend()`、`crbegin()`、`crend()`**（C++11 引入）：
  ```cpp
  const_iterator cbegin() const noexcept;
  const_iterator cend() const noexcept;
  const_reverse_iterator crbegin() const noexcept;
  const_reverse_iterator crend() const noexcept;
  ```
  返回常量版本的迭代器，用于只读遍历。

### 7. **比较操作符**
- **`operator==`、`operator!=`、`operator<` 等**：
  - `vector` 提供标准比较运算符，例如 `==`、`!=`、`<`、`>` 等，用于比较两个 `vector` 的元素。

### 8. **C++11 及之后的增强**
- **`emplace()` 和 `emplace_back()`**：在指定位置直接构造元素，避免不必要的拷贝或移动操作。
- **移动语义**：支持移动构造函数和移动赋值运算符，减少不必要的数据拷贝。

### 9. **示例代码**
以下是一个涵盖了 `std::vector` 主要接口的代码示例：
```cpp
#include <iostream>
#include <vector>

int main() {
    std::vector<int> vec;

    // 添加元素
    vec.push_back(1);
    vec.push_back(2);
    vec.emplace_back(3);

    // 插入元素
    vec.insert(vec.begin() + 1, 4);

    // 访问元素
    std::cout << "Element at index 1: " << vec.at(1) << std::endl;

    // 修改大小
    vec.resize(5, 100);

    // 遍历元素
    for (int value : vec) {
        std::cout << value << " ";
    }
    std::cout << std::endl;

    // 移除元素
    vec.pop_back();
    vec.erase(vec.begin());

    // 交换两个 vector
    std::vector<int> vec2(3, 50);
    vec.swap(vec2);

    // 输出修改后的 vec
    for (int value : vec) {
        std::cout << value << " ";
    }
    std::cout << std::endl;

    return 0;
}
```

### 总结
`std::vector` 提供了丰富的接口用于管理动态数组，包括元素添加、删除、访问、大小调整、容量管理、迭代器遍历等。它在 C++ 开发中非常常用，适合需要频繁插入、删除或者调整大小的动态数据管理场景。通过掌握这些接口，你可以更高效地使用 `std::vector

`，编写出更灵活和更易于维护的代码。

```cpp
#include <iostream>
#include <vector>

int main() {
    // 默认构造
    std::vector<int> my_vector1;

    // 带大小的构造
    std::vector<int> my_vector2(10);// 包含10个默认值初始化的元素
    
    // 带特定初始值的构造
    std::vector<int> my_vector3(10, 2);// 包含10个值为2的元素

    // 拷贝构造函数
    std::vector<int> my_vector4(my_vector3);

    // 添加和删除元素
    my_vector1.push_back(1);
    my_vector.emplace_back(2);

    std::cout << "first element:" << my_vector1[0];
}

```
2. deque
    双端队列，支持快速随机访问，可以在两端高效插入删除元素。
3. list
    双向链表，插入和删除效率高，但不支持快速随机访问。
4. array
    静态数组，大小固定。
5. forward_list
    单向链表，与list类似，但只有单向链接，内存占用小。


## Associative Containers 关联容器
1. set
    集合，存储不相同的元素，内部有序，基于红黑树实现。支持高效的插入、删除、查找。
2. multiset
    多重集合，与set类似，但可以存储重复元素。
3. map
    键值对存储，键是唯一的，基于红黑树实现。适合存储和快速查找映射关系。
4. multimap
    多重映射，与map类似，可以存储重复键。

## Unordered Containers 无序关联容器 （基于哈希表）
1. unordered_set
    无序集合，插入、删除、查找的平均时间复杂度为O(1)。
2. unordered_map
    无序映射，提供键值对的无序存储。
3. unordered_multiset
    多重无序集合，允许重复元素。
4. unordered_multimap
    多重无序映射，允许重复键。
