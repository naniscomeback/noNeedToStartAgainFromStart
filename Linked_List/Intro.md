# 🔗 Singly Linked List: Core Concepts & Operations

A comprehensive, high-density reference guide for Singly Linked Lists (SLL). This document covers foundational architecture, time complexities, and clean Python implementations for core operations.

---

## 📐 1. Introduction to Singly Linked List

A **Singly Linked List** is a linear data structure where elements are not stored in contiguous memory locations. Instead, each element (called a **Node**) points to the next one dynamically.

### Anatomy of a Node
Each node consists of two fields:
1. **Data**: The actual value stored in the node.
2. **Next Pointer**: A reference/pointer to the succeeding node in the sequence. The last node points to `None` (`Null`), signaling the end of the list.

```text
 [ Head ] 
    │
    ▼
┌───────┬──────┐       ┌───────┬──────┐       ┌───────┬──────┐
│ Data1 │ Next ├──────►│ Data2 │ Next ├──────►│ Data3 │ None │
└───────┴──────┘       └───────┴──────┘       └───────┴──────┘
```

### Core Characteristics
* **Dynamic Size**: Allocation happens at runtime. No need to pre-allocate memory like arrays.
* **No Memory Wastage**: Memory is allocated as needed, though it carries an overhead for storing pointers.
* **Sequential Access**: Direct index access ($O(1)$) is impossible. You must traverse from the `Head` ($O(n)$).

### Base Node Implementation
```python
class Node:
    def __init__(self, data):
        self.data = data
        self.next = None

class LinkedList:
    def __init__(self):
        self.head = None
```

---

## ⚡ 2. Core Operations & Implementations

### 📥 A. Insertion at the Head
Adds a new node at the very beginning of the linked list. This becomes the new `Head`.

* **Algorithm**: 
  1. Create a new node.
  2. Point the new node's `next` to the current `head`.
  3. Update the `head` pointer of the list to this new node.
* **Time Complexity**: $O(1)$ — No shifting of elements required.
* **Space Complexity**: $O(1)$

```python
def insert_at_head(self, data):
    new_node = Node(data)
    new_node.next = self.head
    self.head = new_node
```

---

### 📤 B. Deletion of the Head
Removes the first node of the linked list and updates the next node as the new `Head`.

* **Algorithm**:
  1. Check if the list is empty (`head is None`). If so, return.
  2. Hold the current head in a temporary variable (optional, for memory cleanup).
  3. Move the `head` pointer forward to `head.next`.
* **Time Complexity**: $O(1)$
* **Space Complexity**: $O(1)$

```python
def delete_head(self):
    if not self.head:
        return None
    
    # Move head pointer to the next node
    self.head = self.head.next
```

---

### 📏 C. Find the Length of the Linked List
Counts the total number of nodes present in the list.

* **Algorithm**:
  1. Initialize a counter to `0` and a pointer `current` to the `head`.
  2. Loop while `current` is not `None`.
  3. Increment the counter and move `current` to `current.next`.
* **Time Complexity**: $O(n)$ — Must touch every node once.
* **Space Complexity**: $O(1)$

```python
def get_length(self):
    count = 0
    current = self.head
    while current:
        count += 1
        current = current.next
    return count
```

---

### 🔍 D. Search in a Linked List
Determines whether a target value exists within the linked list.

* **Algorithm**:
  1. Start a pointer `current` at the `head`.
  2. Traverse the list checking if `current.data == target`.
  3. Return `True` if found; otherwise, move to `current.next`.
  4. Return `False` if the loop finishes without finding the value.
* **Time Complexity**: $O(n)$ (Worst/Average Case)
* **Space Complexity**: $O(1)$

```python
def search(self, target):
    current = self.head
    while current:
        if current.data == target:
            return True
        current = current.next
    return False
```

---

## 📊 Summary Cheat Sheet


| Operation | Time Complexity | Space Complexity | Key Mechanic |
| :--- | :--- | :--- | :--- |
| **Insert at Head** | $O(1)$ | $O(1)$ | Update pointer to current head |
| **Delete Head** | $O(1)$ | $O(1)$ | Move head pointer forward |
| **Get Length** | $O(n)$ | $O(1)$ | Linear traversal counter |
| **Search Value** | $O(n)$ | $O(1)$ | Linear item inspection |

---
*Document maintained for coding interview prep and quick structural review.*
