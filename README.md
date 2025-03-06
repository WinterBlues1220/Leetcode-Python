# [Leetcode](https://leetcode.com/)-Python 進階程式設計課程


| | Easy | Medium | Hard | Total |
|:---:|:---:|:---:|:---:|:---:|
| **Accepted** | 2 | 0 | 0 | 2 |
| **Total** | 863 | 1807 | 806 | 3476 |
| **Coverage** | 0 % |0 % | 0 % | 0 % |

## 1. [Two Sum](https://leetcode.com/problems/two-sum/)[Easy]

Two Sum V1(雙for迴圈):
```
class Solution:
    def twoSum(self, nums: List[int], target: int) -> List[int]:
        n = len(nums)
        for i in range(n):
            for j in range(i+1,n):
                if nums[i]+nums[j] == target:
                    return i,j
```
>以for迴圈進行多次運算，直到找出答案為止

Two Sum V2(使用字典):
```
class Solution:
    def twoSum(self, nums: List[int], target: int) -> List[int]:
        complement ={}
        for i, num in enumerate(nums):
            complement[num]=i
        for i, num in enumerate(nums):
            num2 = target-num
            if num2 in complement:
                j = complement[num2]
                if j != i:
                    return [i, j]
```
>以enumerate創建字典，並透過計算補數的方式找出答案


## 9. [Palindrome Number](https://leetcode.com/problems/palindrome-number/)[Easy]

Palindrome Number V1(反轉數字):
```
class Solution:
    def isPalindrome(self, x: int) -> bool:
        if( x < 0 or (x % 10 == 0 and x != 0)):
            return False
        else:
            rNum = 0
            while(x > rNum):
                rNum = rNum * 10 + x % 10
                x = x // 10

            if(x == rNum or x == rNum // 10):
                return True
            else:
                return False

```
>排除特殊情況後，以數學原理來把反轉的數字錄入rNum來進行後續回文數的確認

Palindrome Number V2(反轉字串):
```
class Solution:
    def isPalindrome(self, x: int) -> bool:

        if x < 0:
            return False

        s = str(x)

        return s == s[::-1]
```
>排除特殊情況後，以反轉字串來進行直接比較
