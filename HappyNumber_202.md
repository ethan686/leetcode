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
---> 官方题解的分析：
999 -> 243,3位以下的数字 最大也就能到243 不会再超出去。四位及以上的，会在计算中位数变少
9999999999999 (超过 2^32) 计算出来也就是个4位数。
2^31 - 1  21474836487  算出来也是3位数 260。所以 这个题可以有 大于243的三位数出现，但是只能在243以下循环

time : O(logn)
space : O(logn)

## 快慢指针法
这题其实就是找循环，以及循环的时候是1，还是一个其他值。所以可以使用快慢指针的方法,来找到循环。
如果没有循环，那么先到1的，会持续在1等着慢指针过来。（实际上也是一个循环）
如果到不了1的话，那一定是有一个循环的，毕竟是有限集合，反复调用一定是会重复的。
```
class Solution {
public:
    bool isHappy(int n) {
        int slow = n;
        int fast = n;
        do {
            slow = getSquare(slow);
            fast = getSquare((getSquare(fast)));
        } while(slow != fast);
        return slow == 1;
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
time : O(logn)
space : O(1)
