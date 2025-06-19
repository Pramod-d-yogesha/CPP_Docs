# Data Structure Design for Unique Elements

## Problem Requirements
- Store only unique elements
- Support three operations:
  - insert(x)
  - delete(x) 
  - getRandom()

## Optimal Solution
### Data Structures Used
- `std::unordered_map<int, size_t>` (hash map)
- `std::vector<int>` (dynamic array)

### Time Complexities
| Operation | Complexity |
|-----------|------------|
| insert()  | O(1) avg   |
| delete()  | O(1) avg   |
| getRandom() | O(1)    |

## C++ Implementation
```bash
#include <vector>
#include <unordered_map>
#include <cstdlib>
class RandomizedSet {
private:
    std::unordered_map<int, size_t> map;
    std::vector<int> vec;
    
public:
    bool insert(int x) {
        if (map.count(x)) return false;
        vec.push_back(x);
        map[x] = vec.size() - 1;
        return true;
    }
    bool remove(int x) {
        if (!map.count(x)) return false;
        int last = vec.back();
        vec[map[x]] = last;
        map[last] = map[x];
        vec.pop_back();
        map.erase(x);
        return true;
    }
    
    int getRandom() {
        return vec[rand() % vec.size()];
    }
};
```
## Explanation
- Hash Map tracks each element's position in the vector
- Vector stores elements for random access
- Delete Operation:
1. Swaps target with last element
2. Updates indices

- Removes from both structures
- Alternatives Considered
- std::set: O(log n) operations, no O(1) random access
- std::unordered_set: No random access capability
