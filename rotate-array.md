# 刷题日记

### https://leetcode-cn.com/problems/rotate-array

>189. 旋转数组 给定一个数组，将数组中的元素向右移动 k 个位置，其中 k 是非负数。

1. 暴力解法

```
class Solution {
public:
    void rotate(vector<int>& nums, int k) {
        int last;
        int size = nums.size();
        for (int i = 0; i < k; i++) {
            last = nums[size - 1];
            for (int j = size - 1; j > 0; j--) {
                nums[j] = nums[j - 1];
            }
            nums[0] = last;
        }
    }
};
```
解题思路：

- 遍历k次，每次记录数组最后一位
- 将数组其他位置依次向后移动一位
- 移动完成后将首位置替换为记录的最后一位

附加：最暴力的解法往往是不太好的，时间复杂度是 `O(n*k)`，空间复杂度 `O(1)`, 虽然测试用例通过了，但是正式提交时测试用例数据规模增多，导致执行超时了。

2. 使用额外的空间

```
class Solution {
public:
    void rotate(vector<int>& nums, int k) {
        int size = nums.size();
        int temp[size];
        for (int i = 0; i < size; i++) {
            temp[(i + k) % size] = nums[i];
        }
        for (int i = 0; i < size; i++) {
            nums[i] = temp[i];
        }
    }
};
```
解题思路：

- 创建一个新数组，并将偏移k位置后的元素依次放到这个心数组中
- 将新数组拷贝回原数组

附加：时间复杂度 `O(n)`，空间复杂度 `O(n)`，题目上限制不能使用额外的空间，但是提交后依然通过了。

3. 反转法

```
class Solution {
public:
    void reverse(vector<int>& nums, int start, int end) {
        while (start < end) {
            nums[start] = nums[start] + nums[end];
            nums[end] = nums[start] - nums[end];
            nums[start] = nums[start] - nums[end];
            start++;
            end--;
        }
    }
    void rotate(vector<int>& nums, int k) {
        int size = nums.size();
        k = k % size;
        reverse(nums, 0, size - 1);
        reverse(nums, 0, k - 1);
        reverse(nums, k, size - 1);
    }
};
```
解题思路：

- 经过k次旋转后，一定存在0到k%数组长度（因为k有可能大于数组长度，所以取余）在旋转后数组的左边，剩余元素向右移动
- 将元素整体反转，再将左右部分再次反转 即可分别得到旋转后的结果

附加：这个方法不容易被想出来，将注意点集中在结果上，忽略操作细节的一种解题思路，可以做为一种解题思想加入到解题储备库里。
