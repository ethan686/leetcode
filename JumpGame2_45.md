## description
![image](https://github.com/ethan686/leetcode/assets/73508499/fd46e8e3-7100-4bb7-ab13-33b861307a49)

## self_solution
```
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
```
存储每一个元素最短到达n - 1的元素所需要的步数。
1. 从倒数第二个元素开始，确认是否能一步到达最后的n - 1的位置
2. 如果能到达，则记录当前元素对应的最短步数为1
3. 如果不能直接一步到达，则遍历当前元素能走到的位置，对应的最短步数。如果其中出现了1步的，直接更新当前元素最短步数为2，结束当前元素。如果没有1步的，则遍历找到步数最少的一个，+1后保存到当前元素所对应的最短的步数。
4. 最后返回minJmp[0]的值，就是从最开始走所能走到的最短的步数。
time: O(n^2)
space: O(n)
