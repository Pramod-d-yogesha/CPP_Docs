## STLS Details

| STL Container            | Properties_____________________________ | Underlying_Data_Structure | Insert       | Delete       | Find         | Iteration   | Memory Overhead | Ordering  | Duplicates | Random Access | Thread Safety |
|--------------------------|----------------------------------------|---------------------------|--------------|--------------|--------------|-------------|-----------------|-----------|------------|---------------|---------------|
| `std::vector`          | Dynamic array                          | Contiguous array          | O(1) end¹    | O(1) end     | O(n)         | O(1)        | Low             | Insertion | Allowed    | O(1)          | No²           |
| `std::deque`           | Double-ended queue                     | Chunked array             | O(1) ends    | O(1) ends    | O(n)         | O(1)        | Medium          | Insertion | Allowed    | O(1)          | No            |
| `std::list`            | Doubly-linked list                     | Linked nodes              | O(1)         | O(1)         | O(n)         | O(1)        | High            | Insertion | Allowed    | No            | No            |
| `std::forward_list`    | Singly-linked list                     | Linked nodes              | O(1)         | O(1)³        | O(n)         | O(1)        | Medium          | Insertion | Allowed    | No            | No            |
| `std::set`            | Unique sorted elements                 | Red-Black Tree            | O(log n)     | O(log n)     | O(log n)     | O(n)        | High            | Sorted    | No         | No            | No            |
| `std::multiset`       | Allows duplicate sorted elements       | Red-Black Tree            | O(log n)     | O(log n)     | O(log n)     | O(n)        | High            | Sorted    | Yes        | No            | No            |
| `std::unordered_set`  | Unique hashed elements                 | Hash table                | O(1) avg     | O(1) avg     | O(1) avg     | O(n)        | Medium          | Hashed    | No         | No            | No            |
| `std::unordered_multiset` | Allows duplicate hashed elements    | Hash table                | O(1) avg     | O(1) avg     | O(1) avg     | O(n)        | Medium          | Hashed    | Yes        | No            | No            |
| `std::map`            | Key-value pairs, sorted by key         | Red-Black Tree            | O(log n)     | O(log n)     | O(log n)     | O(n)        | High            | Sorted    | Unique keys| No            | No            |
| `std::multimap`       | Allows duplicate sorted keys           | Red-Black Tree            | O(log n)     | O(log n)     | O(log n)     | O(n)        | High            | Sorted    | Dupe keys  | No            | No            |
| `std::unordered_map`  | Key-value pairs, hashed                | Hash table                | O(1) avg     | O(1) avg     | O(1) avg     | O(n)        | Medium          | Hashed    | Unique keys| No            | No            |
| `std::unordered_multimap` | Allows duplicate hashed keys        | Hash table                | O(1) avg     | O(1) avg     | O(1) avg     | O(n)        | Medium          | Hashed    | Dupe keys  | No            | No            |
| `std::stack`          | LIFO container adapter                 | (Uses underlying)         | O(1)         | O(1)         | No           | No          | Depends         | LIFO      | Allowed    | No            | No            |
| `std::queue`          | FIFO container adapter                 | (Uses underlying)         | O(1)         | O(1)         | No           | No          | Depends         | FIFO      | Allowed    | No            | No            |
| `std::priority_queue` | Sorted queue (max-heap by default)     | Heap structure            | O(log n)     | O(log n)     | O(n)         | No          | Medium          | Sorted    | Allowed    | No            | No            |

**Footnotes:**
1. `O(n)` for middle insertions due to shifting
2. Thread-safe only for read operations
3. Requires predecessor node access

## STLs Selection Based On Requirments
| STL Container            | When to Choose                          | Why Choose It                                                                 | Real-World Use Case                     |
|--------------------------|----------------------------------------|-------------------------------------------------------------------------------|-----------------------------------------|
| `std::vector`           | Need dynamic array with random access  | - Cache-friendly contiguous storage<br>- O(1) amortized push_back<br>- O(1) random access | Game entity storage, CSV data loading   |
| `std::deque`            | Frequent insertions at both ends       | - O(1) push/pop front/back<br>- Chunked storage avoids reallocation           | Message queue, Undo/Redo buffers        |
| `std::list`             | Frequent middle insertions/deletions   | - O(1) insert/delete anywhere<br>- No iterator invalidation                    | Browser history, Genetic algorithm populations |
| `std::forward_list`     | Memory-constrained sequential access   | - No back pointer (saves memory)<br>- O(1) insertion after known position      | Embedded systems, Parser token chains   |
| `std::set`              | Maintain sorted unique elements        | - Automatic sorting<br>- O(log n) search/insert                                | Dictionary words, Sorted leaderboard    |
| `std::multiset`         | Sorted collection with duplicates      | - Allows duplicates while maintaining order                                    | Student grade records, Sensor value logs |
| `std::unordered_set`    | Fast lookup without ordering           | - O(1) average operations<br>- Hash-based efficiency                          | Username database, Spellchecker dictionary |
| **`std::unordered_multiset`** | Fast lookup with duplicates, no order | - O(1) average operations<br>- Allows duplicate elements                       | Word frequency counter, Log analysis    |
| `std::map`              | Key-value pairs with sorted keys       | - Binary search tree structure<br>- Ordered traversal                          | Configuration settings, Language dictionaries |
| `std::multimap`         | Sorted key-value with duplicates       | - Allows duplicate keys<br>- Maintains sorting                                 | Student course registrations, Book index |
| `std::unordered_map`    | Fast key-value access                  | - O(1) average access<br>- Ideal for frequent lookups                         | HTTP header storage, Cache implementations |
| **`std::unordered_multimap`** | Fast key-value with duplicates      | - O(1) average access<br>- Allows duplicate keys                              | HTTP query parameters, Database indices |
| `std::stack`            | LIFO (Last-In-First-Out) needs         | - Simple interface (push/pop/top)<br>- Adapts underlying container            | Function call stack, Expression evaluation |
| `std::queue`            | FIFO (First-In-First-Out) processing   | - Fair ordering<br>- Constant time operations                                  | Printer job queue, Breadth-first search |
| `std::priority_queue`   | Always need max/min element            | - Heap structure efficiency<br>- O(log n) insert/extract                       | Dijkstra's algorithm, Hospital triage   |


---

# Key Selection Criteria:
## Access Patterns:
-Random access → vector/deque
-Sequential access → list/forward_list

## Ordering Needs:
- Sorted → set/map
- Unordered → unordered_set/unordered_map

## Memory Constraints:
- Minimal overhead → vector
- Compact storage → forward_list

## Modification Frequency:
- Frequent inserts/deletes → list/unordered_map
- Stable structure → vector/array

## Special Requirements:
- Thread safety → None natively (need mutexes)
- Cache locality → vector/array

## Pro Tips:
- 90% of cases: Start with vector or unordered_map
- Sorting needed: Switch to set/map
- Memory-critical: Consider forward_list
- Order preservation: list maintains insertion order


### std::unordered_multiset
- Use when you need: Duplicate elements + fastest lookup
- Example: Counting word occurrences in documents

### std::multimap
- Use when you need: Multiple values per sorted key
- Example: { "John" : [90, 85, 92], "Alice" : [88, 95] }

### std::unordered_multimap
- Use when you need: Multiple values per unsorted key
- Example: { "search_term" : [result1, result2], "filter" : [valueA, valueB] }
