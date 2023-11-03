## description 
![image](https://github.com/ethan686/leetcode/assets/73508499/626a166c-2f8b-4eac-8ba8-8a7586fc7e13)
## self_solution
```
class Solution {
public:
    bool isIsomorphic(string s, string t) {
        if(s.size() != t.size()) {
            return false;
        }
        int n = s.size();

        std::unordered_map<char, char> replaceStr;
        std::unordered_map<char, bool> ifUsed;
        for(int i = 0; i < n; i++) {
            if(!replaceStr.count(s[i])) {
                if(ifUsed.count(t[i]) && ifUsed[t[i]] == true) {
                    return false;
                }
                replaceStr[s[i]] = t[i];
                ifUsed[t[i]] = true;
            } else {
                if(replaceStr[s[i]] != t[i]) {
                    return false;
                }
            }
        }
        return true;
    }
};
```
思路：用了两个哈希表。遍历两个字符串，为s中的元素和t中的元素建立hash映射。并且建立映射时，确保t中元素没有被其他的s使用过。
遍历过程中确保s中的元素均可以被t中的元素映射，且彼此之间的映射关系不存在冲突。
time:O(n)
space:2O(n) -> O(n)
## other_solution
```
class Solution {
public:
    bool isIsomorphic(string s, string t) {
        int n = s.size();
        int m = t.size();
        if(n != m) {
            return false;
        }
        for(int i = 0; i < n; i++) {
            if(s.find(s[i]) != t.find(t[i])) {
                return false;
            }
        }
        return true;
    }
};
```
遍历的过程中，查找s和t当前需要比较的元素在整个串中的index值，如果是同构的，那么对应的index在整个字符串中出现的位置一定是相同的。
time: O(n * n)
space: O(1)
