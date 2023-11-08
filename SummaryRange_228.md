## description
![image](https://github.com/ethan686/leetcode/assets/73508499/cfbd269c-63b6-4f95-94f5-61f0f0567d57)
## self_solution
```
class Solution {
public:
    vector<string> summaryRanges(vector<int>& nums) {
        vector<string> result;
        std::string str = "";
        int n = nums.size();
        if(n == 0) {
            return result;
        }
        bool isSeq = false;
        for(int i = 0; i < n; i++) {
            if(i == 0) {
                str += to_string(nums[i]);
                continue;
            }
            if(nums[i] == nums[i - 1] + 1) {
                if(isSeq) {
                    for(int j = str.size() - 1; j >= 0; j--) {
                        if(str[j] == '>') {
                            break;
                        }
                        str.pop_back();
                    }
                    str += to_string(nums[i]);
                } else {
                    str.push_back('-');
                    str.push_back('>');
                    str += to_string(nums[i]);
                }
                isSeq = true;
            } else {
                result.push_back(str);
                str.clear();
                str += to_string(nums[i]);
                isSeq = false;
            }
        }
        result.push_back(str);
        return result;
    }
};
```
if(nums[i] - nums[i - 1] == 1) 
注意这里可能会出现边界的用例。2147483647 - (-2147483647)等会超过int.需要修改为 nums[i] == nums[i-1] + 1

## 官方-分组循环
```
class Solution {
public:
    vector<string> summaryRanges(vector<int>& nums) {
        vector<string> result;
        int i = 0;
        int n = nums.size();
        while(i < n) {
            int low = i;
            i++;
            while(i < n && nums[i] == nums[i - 1] + 1) {
                i++;
            }
            int high = i - 1;
            string str = to_string(nums[low]);
            if(low < high) {
                str.append("->");
                str.append(to_string(nums[high]));
            }
            result.push_back(move(str));
        }
        return result;
    }
};
```
实际上并不需要把每一个小区间内部的所有数据都push 又 pop。循环中把一个小区间的左右边界找出来就可以了。
找出来之后，找出来左右边界对应的值，构建对应的string。这样不需要考虑最后一段区间的逻辑。

