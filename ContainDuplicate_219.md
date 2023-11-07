## description 
![image](https://github.com/ethan686/leetcode/assets/73508499/28e96c07-e6b4-436e-8b0a-44ab763195cf)
## self_solution
```
class Solution {
public:
    bool containsNearbyDuplicate(vector<int>& nums, int k) {
        unordered_map<int, int> indexMap;
        for(int i = 0; i < nums.size(); i++) {
            if(indexMap.count(nums[i])) {
                int diff = i - indexMap[nums[i]];
                if(diff <= k) {
                    return true;
                }
                indexMap[nums[i]] = i;
            } else {
                indexMap[nums[i]] = i;
            }
        }
        return false;
    }
};
```
使用哈希表存储index值作为辅助，一次遍历，如果已有相同nums的值。比较index的差值和k的关系

time : O(n)
space : O(n)

## 滑动窗口的解法
实际上i 和 j 下标的差值，对应了数组的滑动窗口的大小。按照滑动窗口，判断窗口中是否存在重复元素。
由于需要判断窗口中是否存在重复值，可以使用hashSet的数据结构。
```
class Solution {
public:
    bool containsNearbyDuplicate(vector<int>& nums, int k) {
        unordered_set<int> s;
        for(int i = 0; i < nums.size(); i++) {
            if(s.count(nums[i])) {
                return true;
            }
            s.emplace(nums[i]);
            if(s.size() > k) {
                s.erase(nums[i - k]);
            }
        }
        return false;
    }
};
```
1. 判断当前新看到的元素，是否在集合中，如果在，直接认为满足条件
2. 如果不在，将当前元素放到集合中
3. 将集合开头元素去除
注意：这里的集合长度和k相同，但是题目要求 下标差值<=k 所以并不是窗口内部要重叠。可以是窗口旁边的一个和窗口内部的元素之间比较
time : O(n)
space : O(k)
