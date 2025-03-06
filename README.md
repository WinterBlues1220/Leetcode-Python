# [Leetcode](https://leetcode.com/)-Python 進階程式設計課程


| | Easy | Medium | Hard | Total |
|:---:|:---:|:---:|:---:|:---:|
| **Accepted** | 1 | 0 | 0 | 1 |
| **Total** | 863 | 1807 | 806 | 3476 |
| **Coverage** | 0 % |0 % | 0 % | 0 % |

## 1.[Two Sum](https://leetcode.com/problems/two-sum/)

Two Sum V1:
```
class Solution:
    def twoSum(self, nums: List[int], target: int) -> List[int]:
        n = len(nums)
        for i in range(n):
            for j in range(i+1,n):
                if nums[i]+nums[j] == target:
                    return i,j
```

Two Sum V2:
```
class Solution:
    def twoSum(self, nums: List[int], target: int) -> List[int]:
        complement ={}
        for i, num in enumerate(nums): # a dictionary
            complement[num]=i
        for i, num in enumerate(nums):
            num2 = target-num
            if num2 in complement:
                j = complement[num2]
                if j != i:
                    return [i, j]
```
