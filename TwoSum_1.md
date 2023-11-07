## description
![image](https://github.com/ethan686/leetcode/assets/73508499/b32cc42f-b127-4b95-9e57-ce005efd86fa)
## self_solution
```
class Solution {
public:
    vector<int> twoSum(vector<int>& nums, int target) {
        vector<int> result;
        unordered_map<int, int> helpMap;
        for(int i = 0; i < nums.size(); i++) {
            if(helpMap.count(target - nums[i])) {
                result.push_back(i);
                result.push_back(helpMap[target - nums[i]]);
                return result;
            }
            helpMap[nums[i]] = i;
        }
        return result;
    }
};
```
正常的思路O(n2)的两层循环就可以找出来。这里使用了一个哈希表来空间换时间。
1. 遍历过程中，将当前的值和下标作为键值对 存放再哈希表中
2. 遍历过程中，如果当前target-当前元素值在哈希表中，说明已经找到，返回两个下标即可。

time : O(n)
space : O(n)
