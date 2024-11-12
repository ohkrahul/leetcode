# LRU Cache

## Problem Link
[LeetCode - LRU Cache](https://leetcode.com/problems/lru-cache/)

## Difficulty
Medium

## Problem Description
<p>Design a data structure that follows the constraints of a <strong><a href="https://en.wikipedia.org/wiki/Cache_replacement_policies#LRU" target="_blank">Least Recently Used (LRU) cache</a></strong>.</p>

<p>Implement the <code>LRUCache</code> class:</p>

<ul>
	<li><code>LRUCache(int capacity)</code> Initialize the LRU cache with <strong>positive</strong> size <code>capacity</code>.</li>
	<li><code>int get(int key)</code> Return the value of the <code>key</code> if the key exists, otherwise return <code>-1</code>.</li>
	<li><code>void put(int key, int value)</code> Update the value of the <code>key</code> if the <code>key</code> exists. Otherwise, add the <code>key-value</code> pair to the cache. If the number of keys exceeds the <code>capacity</code> from this operation, <strong>evict</strong> the least recently used key.</li>
</ul>

<p>The functions <code>get</code> and <code>put</code> must each run in <code>O(1)</code> average time complexity.</p>

<p>&nbsp;</p>
<p><strong class="example">Example 1:</strong></p>

<pre>
<strong>Input</strong>
[&quot;LRUCache&quot;, &quot;put&quot;, &quot;put&quot;, &quot;get&quot;, &quot;put&quot;, &quot;get&quot;, &quot;put&quot;, &quot;get&quot;, &quot;get&quot;, &quot;get&quot;]
[[2], [1, 1], [2, 2], [1], [3, 3], [2], [4, 4], [1], [3], [4]]
<strong>Output</strong>
[null, null, null, 1, null, -1, null, -1, 3, 4]

<strong>Explanation</strong>
LRUCache lRUCache = new LRUCache(2);
lRUCache.put(1, 1); // cache is {1=1}
lRUCache.put(2, 2); // cache is {1=1, 2=2}
lRUCache.get(1);    // return 1
lRUCache.put(3, 3); // LRU key was 2, evicts key 2, cache is {1=1, 3=3}
lRUCache.get(2);    // returns -1 (not found)
lRUCache.put(4, 4); // LRU key was 1, evicts key 1, cache is {4=4, 3=3}
lRUCache.get(1);    // return -1 (not found)
lRUCache.get(3);    // return 3
lRUCache.get(4);    // return 4
</pre>

<p>&nbsp;</p>
<p><strong>Constraints:</strong></p>

<ul>
	<li><code>1 &lt;= capacity &lt;= 3000</code></li>
	<li><code>0 &lt;= key &lt;= 10<sup>4</sup></code></li>
	<li><code>0 &lt;= value &lt;= 10<sup>5</sup></code></li>
	<li>At most <code>2 * 10<sup>5</sup></code> calls will be made to <code>get</code> and <code>put</code>.</li>
</ul>


## Test Cases
```
["LRUCache","put","put","get","put","get","put","get","get","get"]
[[2],[1,1],[2,2],[1],[3,3],[2],[4,4],[1],[3],[4]]
```

## Initial Template
```python
# Code template not available
```

## Solution
## 1. Initial Thoughts
### Problem analysis
- This problem asks for designing a data structure that follows the constraints of an LRU (Least Recently Used) cache.
- The LRU cache is a technique used to store frequently used data in order to improve performance by reducing the number of times data needs to be fetched from a slower storage system.
- When the cache is full and a new item needs to be added, the least recently used item is evicted from the cache.

### Key observations
- A typical implementation of an LRU cache involves using a hash table to store the key-value pairs and a doubly linked list to maintain the order of the items.
- The hash table allows for fast lookup by key in O(1) time.
- The doubly linked list allows for efficient insertion and removal of items, also in O(1) time.

### Possible approaches
- One approach is to implement the cache from scratch using a hash table and a doubly linked list.
- Another approach is to leverage built-in data structures that already provide the necessary functionality, such as a `collections.OrderedDict` in Python.

## 2. Solution Implementation
```python
class LRUCache:
    def __init__(self, capacity: int):
        self.capacity = capacity
        self.cache = {}  # Key-value pairs
        self.keys = []  # List of keys in usage order

    def get(self, key: int) -> int:
        if key in self.cache:
            # Move the key to the end of the list
            self.keys.remove(key)
            self.keys.append(key)
            return self.cache[key]
        else:
            return -1

    def put(self, key: int, value: int) -> None:
        if key in self.cache:
            # Move the key to the end of the list
            self.keys.remove(key)
            self.keys.append(key)
            self.cache[key] = value
        else:
            if len(self.cache) == self.capacity:
                del self.cache[self.keys.pop(0)]  # Remove oldest key
            self.cache[key] = value
            self.keys.append(key)
```

## 3. Solution Explanation
### How the solution works
- The `__init__` method initializes the cache with the specified capacity and creates a hash table and a list.
- The `get` method checks if the key exists in the cache. If it does, it moves the key to the end of the list to indicate that it's recently used.
- The `put` method checks if the key exists in the cache. If it does, it moves the key to the end of the list to indicate that it's recently used. If the key doesn't exist and the cache is at capacity, it removes the oldest key (from the front of the list) to make room for the new key.

### Key steps and logic explained
1. `get` method:
   - Check if the key exists in the cache.
   - If it does, move the key to the end of the list.
   - Return the value associated with the key or -1 if it doesn't exist.
2. `put` method:
   - Check if the key exists in the cache.
   - If it does, move the key to the end of the list.
   - If the key doesn't exist and the cache is at capacity, remove the oldest key to make room for the new key.
   - Add the new key and value to the cache.

### Why this approach is effective
- This approach uses a hash table for fast lookup and a list for maintaining the order of items.
- The operations of moving a key to the end of the list or removing the oldest key can be done in O(1) time.
- The hash table allows for fast lookup by key, also in O(1) time.
- This design adheres to the constraints of an LRU cache and provides efficient access to frequently used data.

## 4. Complexity Analysis
### Time complexity
- `get` method: O(1) average lookup time with a hash table.
- `put` method: O(1) average update time with hash table and list operations.

### Space complexity
- O(capacity), where `capacity` is the maximum number of key-value pairs that the cache can hold.

## Topics
Hash Table, Linked List, Design, Doubly-Linked List

## Author
[ohkrahul](https://github.com/ohkrahul)

Solved on: 2024-11-12
