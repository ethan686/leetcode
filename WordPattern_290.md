## description
![image](https://github.com/ethan686/leetcode/assets/73508499/aa309256-1007-4d06-ad11-b2d3e663b455)
## self_solution
```
class Solution {
public:
    bool wordPattern(string pattern, string s) {
        std::vector<std::string> words;
        std::string word;
        for(int i = 0; i < s.size(); i++) {
            if(s[i] == ' ' && !word.empty()) {
                words.push_back(word);
                word = "";
                continue;
            }
            word.push_back(s[i]);
        }
        if(!word.empty()) {
            words.push_back(word);
        }

        int n = pattern.size();
        int m = words.size();
        if(n != m) {
            return false;
        }
        std::unordered_map<char, std::string> pattern2s;
        std::unordered_map<std::string, bool> ifUsed;
        for(int i = 0; i < n; i++) {
            if(!pattern2s.count(pattern[i])) {
                if(ifUsed.count(words[i]) && ifUsed[words[i]] == true) {
                    return false;
                }
                pattern2s[pattern[i]] = words[i];
                ifUsed[words[i]] = true;
            } else {
                if(pattern2s[pattern[i]] != words[i]) {
                    return false;
                }
            }
        }
        return true;
    }
};
```
1. 先将单词从字符串中挨个抽离出来
2. 判断pattern中字符个数与单词个数是否相同，不同直接return false
3. 双向映射pattern以及words，是否可以通过unordered_map关联起来

time:O(n + m)
space:O(n + 2m)
