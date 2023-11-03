## description 
![image](https://github.com/ethan686/leetcode/assets/73508499/7820b37a-74e4-4795-8719-bf92d21466ec)

## self_solution
```
class Solution {
public:
    vector<vector<string>> groupAnagrams(vector<string>& strs) {
        vector<vector<string>> strGroup;
        unordered_map<string, vector<string>> res;
        for(const auto& str : strs) {
            string sortStr = str;
            sort(sortStr.begin(), sortStr.end());
            res[sortStr].push_back(str);
        }
        for(auto it = res.begin(); it != res.end(); it++) {
            strGroup.push_back(it->second);
        }
        return strGroup;
    }
};
```
有点偷懒的做法了。
1. 建立一个string 和 vector的哈希表
2. 遍历strs数组，对于其中每一个str进行排序，排序之后的str作为键值，将原str存到对应的vector中
3. 遍历哈希表，将每一个vector取出

time : O(n*mlogm)
space : O(nm)

## other_solution
将每一个字符串中出现过的字符的频次进行计数。利用这个频次的计数数组作为key值，进行判断。
time : O(n * m)
space : O(nm)
