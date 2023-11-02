## description.
![Uploading image.png…]()

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
brute, 题目实际上就是找数组大小范围内，大于每一个数的