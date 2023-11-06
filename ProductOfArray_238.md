## description 
![image](https://github.com/ethan686/leetcode/assets/73508499/5ca62d52-028e-4e82-8d17-8b25a78f7546)
## self_solution
```
class Solution {
public:
    vector<int> productExceptSelf(vector<int>& nums) {
        int n = nums.size();
        vector<int> res(n, 1);
        vector<int> prefix(n, 1);
        vector<int> suffix(n, 1);

        for(int i = 0; i < n; i++) {
            if(i == 0) {
                prefix[i] = 1;
            } else {
                prefix[i] = prefix[i - 1] * nums[i - 1];
            }
        }

        for(int i = n - 1; i >=0; i--) {
            if(i == n - 1) {
                suffix[i] = 1;
            } else {
                suffix[i] = suffix[i + 1] * nums[i + 1];
            }
        }

        for(int i = 0; i < n; i++) {
            res[i] = prefix[i] * suffix[i];
        }
        
        return res;
    }
};
```
题目中提示了前缀乘积和后缀乘积。可以把题目要求的除当前元素外所有的乘积，划分成前缀乘积 * 后缀乘积。
1. 从前向后遍历，对于每一个i，获取其前所有元素的乘积
2. 从后向前遍历，对于每一个i，获取其后所有元素的乘积
3. 对于前缀第一个元素和后缀最后一个元素 的乘积设置为1
4. 将对应位置的前缀乘积和后缀乘积相乘

time : O(n)
space : O(n)
