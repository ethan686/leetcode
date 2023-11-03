## description
![image](https://github.com/ethan686/leetcode/assets/73508499/a3ac26c3-4d89-46a0-9008-8b96f635ce4b)
## self_solution
```
class Solution {
public:
    bool canConstruct(string ransomNote, string magazine) {
        vector<int> chars(26);
        for(const auto& c : magazine) {
            chars[c - 'a']++;
        }

        for(const auto& c : ransomNote) {
            if(chars[c - 'a']-- > 0) {
                continue;
            } else {
                return false;
            }
        }
        return true;
    }
};
```
简单的hash，先记录下来magazine中包含哪些字符以及字符的出现频次。
再遍历ransomNote，在chars中找是否已有该元素，并进行--。一旦出现某个字符无法被已有chars中的元素cover住 报错退出。
全部都能找到ransomNote，可以被成功构建。

time:2O(n) -> O(n)
space:O(1)
