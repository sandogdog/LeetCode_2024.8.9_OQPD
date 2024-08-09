前言：之前在别的平台写了几天博客，虽然流量高，但是感觉认可度不如GitHub。嗯，我会努力写博客的。

---
下面为LeetCode 2024/8/9 每日1题 

3132.找出与数组相加的整数Ⅱ（中等）
给你两个整数数组 nums1 和 nums2。
从 nums1 中移除两个元素，并且所有其他元素都与变量 x 所表示的整数相加。如果 x 为负数，则表现为元素值的减少。
执行上述操作后，nums1 和 nums2**相等**。当两个数组中包含相同的整数，并且这些整数出现的频次相同时，两个数组**相等**。
返回能够实现数组相等的**最小**整数 x 。
---
示例 1:
输入：nums1 = [4,20,16,12,8], nums2 = [14,18,10]
输出：-2
解释：
移除 nums1 中下标为 [0,4] 的两个元素，并且每个元素与 -2 相加后，nums1 变为 [18,14,10] ，与 nums2 相等。

---
示例 2:
输入：nums1 = [3,5,5,3], nums2 = [7,7]
输出：2
解释：
移除 nums1 中下标为 [0,3] 的两个元素，并且每个元素与 2 相加后，nums1 变为 [7,7] ，与 nums2 相等。

---
code：
```Java
class Solution {
    public int minimumAddedInteger(int[] nums1, int[] nums2) {
        int m = nums1.length, n = nums2.length;
        Arrays.sort(nums1);
        Arrays.sort(nums2);
        for (int i: new int[]{2,1,0}) {
            int left = i + 1, right = 1;
            while (left < m && right < n) {
                if (nums1[left] - nums2[right] == nums1[i] - nums2[0]) {
                    ++right;
                }
                ++left;
            }
            if (right == n) {
                return nums2[0] - nums1[i];
            }
        }
        return 0;
    }
}
```
---
今日总结：

1.为什么是int i: {2, 1, 0}，而不是int i: {0 1, 2}？

因为X可能不止一种情况，要最小的，就要数组一的值最大 x = s2-s1 ，s1大 x就小，所以先枚举更大的情况
（容易遇到的问题）
