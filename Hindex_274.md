## description.
![image](https://github.com/ethan686/leetcode/assets/73508499/35f63ed3-7200-40ea-afb8-e35294f68e25)
 
## self_solution
```
class Solution {
public:
    int hIndex(vector<int>& citations) {
        int n = citations.size();
        int res = 0;
        for(int i = 1; i <= n; i++) {
            int count = 0;
            for(int j = 0; j < n; j++) {
                if(citations[j] >= i) {
                    count++;
                }
            }
            if(count >= i) {
                res = i;
            }
        }
        return res;
    }
};
```
brute. no need to explain
time: O(n^2)
space:O(1)
