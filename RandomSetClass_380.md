## description
![380](https://github.com/ethan686/leetcode/assets/73508499/8eb034bf-9dca-435d-a8ec-2302bb38fdea)
## self_solution 
```
class RandomizedSet {
public:
    RandomizedSet() {
        srand((unsigned)time(NULL));
    }
    
    bool insert(int val) {
        if(indexMap.count(val)) {
            return false;
        }
        nums.push_back(val);
        indexMap[val] = nums.size() - 1;
        return true;
    }
    
    bool remove(int val) {
        if(indexMap.count(val) == 0) {
            return false;
        }
        int lastNum = nums.back();
        int lastPos = indexMap[lastNum];
        int rmvPos = indexMap[val];
        nums[lastPos] = val;
        nums[rmvPos] = lastNum;
        nums.pop_back();
        indexMap[lastNum] = rmvPos;
        indexMap.erase(val);
        return true;
    }
    
    int getRandom() {
        int size = nums.size();
        if(size <= 0) {
            return -1;
        }
        return nums[rand() % size];
    }
private:
    unordered_map<int, int> indexMap;
    vector<int> nums;
};
```
这题关键有两个信息，一个是要保证各个操作的O(1)的时间复杂度，第二个是要保证能够随机获取到现有的一个值。
O(1)的时间复杂度，所以很容易想到需要有哈希表的存在，但是没办法直接在哈希表上进行随机获取一个值，所以还需要有一个辅助的数组，在数组上进行随机获取某一个index对应的取值。

1. 设置一个哈希表，一个变长数组。哈希表中保存 元素的值以及对应在数组中的index
2. 插入的时候，判断哈希表中是否有该元素。若没有，在数组中push进去，并将index保存在哈希表中
3. 删除的时候，判断哈希表中是否无该元素。若有，和数组最后一个元素交换，pop_back最后一个元素。若刚好就是最后一个元素，无非是自己和自己交换，然后删除罢了。当然可以提前优化一下，直接删除
4. 在构造里面进行srand，生成一个种子，然后在getRandom的函数中rand一个下标，实现随机选取的目标。

time : O(1)
space : O(n)
