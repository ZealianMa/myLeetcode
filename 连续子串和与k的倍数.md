### 连续子串和与k的倍数

给你一个整数数组 nums 和一个整数 k ，编写一个函数来判断该数组是否含有同时满足下述条件的连续子数组：

    子数组大小 至少为 2 ，且
    子数组元素总和为 k 的倍数。

如果存在，返回 true ；否则，返回 false 。

如果存在一个整数 n ，令整数 x 符合 x = n * k ，则称 x 是 k 的一个倍数。

 

示例 1：

输入：nums = [23,2,4,6,7], k = 6
输出：true
解释：[2,4] 是一个大小为 2 的子数组，并且和为 6 。

示例 2：

输入：nums = [23,2,6,4,7], k = 6
输出：true
解释：[23, 2, 6, 4, 7] 是大小为 5 的子数组，并且和为 42 。 
42 是 6 的倍数，因为 42 = 7 * 6 且 7 是一个整数。

示例 3：

输入：nums = [23,2,6,4,7], k = 13
输出：false

 

提示：

    1 <= nums.length <= 105
    0 <= nums[i] <= 109
    0 <= sum(nums[i]) <= 231 - 1
    1 <= k <= 231 - 1







#### 解题

```python
class Solution(object):
  def checkSubarraySum(self, nums, k):
    sums = nums
    for numIdx in range(1,len(nums)):
    sums[numIdx] = sums[numIdx] + sums[numIdx-1]
    sums = [i % k for i in sums]
    sumDict = {}
    move = 0
    for i,mod in enumerate(sums):
      if(mod not in sumDict):
        sumDict[mod] = i
      if(mod in sumDict):
        if(i - sumDict[mod] > 1):
          return True
      if(mod == 0 and i > 0):
        return True
    return False
```



挺jb难得 还是要用前缀和 这次加了点前缀和的数学应用 看到别人的代码写得比我干净太多了 好羡慕

还用了个同余定理

最后用立下hash查找 hash查找到没有那么难（之前弄过类似词频统计的） 但是一开始没弄出来 后面用了enumerate方法之后好多了

而且还要善于归纳变量 然后决定哪个变量做键 哪个变量做值 找对了后事半功倍！