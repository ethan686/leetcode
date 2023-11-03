## description
![image](https://github.com/ethan686/leetcode/assets/73508499/454aec2f-9d24-4fae-b826-dfbcf0c7c4f4)
## self_solution 
```
class Solution {
public:
    bool isAnagram(string s, string t) {
        int n = s.size();
        int m = t.size();
        if(n != m) {
            return false;
        }

        std::vector<int> chars(26);
        for(const auto& c : s) {
            chars[c - 'a']++;
        }
        for(const auto& c : t) {
            if(chars[c - 'a']-- <= 0) {
                return false;
            }
        }

        return true;
    }
};
```
1. 比较一下两个字符串中的字符数是否相同，不相同则直接退出。（字符数相同，则可保证只要t字符串被满足了，s也就没有剩余）
2. 建立一个数组，存储s中每一个字符出现的频次。
3. 遍历t，对于t中每一个字符，查看是否有可用的，没有则return false
time : 2O(n)
space : O(1)

## other_solution
直接sort后，看一下是否相同。
time ：O(nlogN)
space: O(nLogN)
