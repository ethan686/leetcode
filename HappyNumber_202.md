## description
![image](https://github.com/ethan686/leetcode/assets/73508499/9405c0b9-be34-4d98-b6b9-59e2dbb4be95)
## self_solution
```
class Solution {
public:
    bool isHappy(int n) {
        unordered_map<int, int> calcRes;
        int tmp = 0;
        while(n) {
            if(calcRes.count(n) && calcRes[n] != 1) {
                return false;
            }
            tmp = getSquare(n);
            if(tmp == 1) {
                return true;
            }
            calcRes[n] = tmp;
            n = tmp;
        }
        return false;
    }
    int getSquare(int n) {
        int res = 0;
        while(n) {
            int num = n % 10;
            res += (num * num);
            n = n/10;
        }
        return res;
    }
};
```
用一个哈希表辅助，防止出现死循环的情况。同时，只要出现循环，如果不是1，那就直接返回false。
对于每一个值，取每一位的平方然后求和。将和当作下一个n值，进行循环判断。出现1，则直接返回true。
注：可能会出现，算出来的和 一直变大的情况(需要数学证明 可能会出现么？？)。
这种情况会无限死循环下去。没有考虑这种情况的处理，但是LC上的用例可以过。

time : O(1) 
