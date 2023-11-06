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

## 二分法
```
class Solution {
public:
    int hIndex(vector<int>& citations) {
        int n = citations.size();
        int left = 0;
        int right = n;
        while(left < right) {
            int mid = (left + right + 1) >> 1;
            if(check(mid, citations)) {
                left = mid;
            } else {
                right = mid - 1;
            }
        }
        return right;
    }

    bool check(int mid, const vector<int>& citations) {
        int cnt = 0;
        for(auto citation : citations) {
            if(citation >= mid) {
                cnt++;
            }
        }
        return cnt >= mid;
    }
};
```
二分方法成立的重要原因是，对于h指数，h+1不满足性质，小于h的所有数又均满足性质。
可以直接二分h，找到h最大的一个满足条件的值。每一次二分的时候，对于找到的h，遍历citations数组，判断是否满足条件。

注意，这个二分是判断最大的一个满足条件的值，需要在取mid的时候 (left + right + 1) >> 1。防止死循环

