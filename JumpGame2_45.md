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

## 官方 greedy
```
class Solution {
public:
    int jump(vector<int>& nums) {
        int n = nums.size();
        int times = 0;
        int border = 0;
        int maxPos = 0;
        for(int i = 0; i < n - 1; i++) {
            maxPos = max(maxPos, nums[i] + i);
            if(i == border) {
                border = maxPos;
                times++;
            }
        }
        return times;
    }
};
```
take 2 3 1 2 4 2 3 as example
和跳跃游戏1的思路上引申出来：从头开始向后遍历，每一个下标位置上进行判断，对应的num[i] + i是不是能走到更远的地方，维护能走到的最远的边界。
一开始在index = 0的位置上，num[0] = 2,在0的时候就要进行第一次跳跃。于此同时更新了当前最远边界为2 以及下一次不得不跳跃点为 index = 2
在从index=0 -> index=2的过程中，不断的更新最远的边界，当走到index = 2的时候，又需要进行跳跃了，但是此时不是根据num[2] + 1来更新下一个跳跃点，而是在这个过程中
找到的最远的边界 作为下一次的跳跃点。
上面的过程，简言之就是 找到了第一次跳跃能带来的最远的下一个跳跃终点。至于是在哪个地方进行跳跃的 是无所谓的，因为都在跳跃的区间内部 或闭区间上。
注意，不要走到 n - 1.在这个位置上 再进行上述逻辑已经没有意义了，能到这里，已经完成人恩物了。
1. index = 0 ，进行第一次跳跃，记录最远到达的位置是index = 2
2. index = 1 ，计算最远的位置为 4，更新最远位置为4
3. index = 2 ，计算最远的位置为 3，不更新最远的位置。达到第一次规定的跳跃点，跳跃次数++，更新下一次跳跃位置为index = 4
4. index = 3 ，计算最远的位置为 5，更新最远位置为5
5. index = 4 ，计算最远的位置为 8，更新最远位置为8。到达第二次规定的跳跃点，跳跃次数++，更新下一次跳跃位置为index = 8(已经满足)
6. index = 5 ，计算最远的位置为 7，不更新最远的位置。
7. index = 6 ，结束循环

