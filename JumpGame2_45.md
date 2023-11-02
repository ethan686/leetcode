##description
![image](https://github.com/ethan686/leetcode/assets/73508499/fd46e8e3-7100-4bb7-ab13-33b861307a49)

...
class Solution {
public:
    int jump(vector<int>& nums) {
        int n = nums.size();
        if(n == 1) {
            return 0;
        }
        if(n == 2 && nums[0] >= 1) {
            return 1;
        }
        std::vector<int> minJump(n, 10000);
        minJump[n - 1] = 0;
        for(int i = n - 2; i >= 0; i--) {
            if(nums[i] + i >= n - 1) {
                minJump[i] = 1;
            } else {
                int tempMin = 10000;
                for(int j = i + 1; j <= i + nums[i]; j++) {
                    if(minJump[j] == 1) {
                        tempMin = 2;
                        break;
                    }
                    tempMin = min(tempMin, minJump[j] + 1);
                }
                minJump[i] = tempMin;
            }
        }
        return minJump[0];
    }
};
...
