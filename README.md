# [Leetcode](https://leetcode.com/) - 進階程式設計課程


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

Two Sum V3(使用Golang):
```
func twoSum(nums []int, target int) []int {
    for i := 0; i < len(nums); i++ {
        for j := i + 1; j < len(nums); j++ {
            if nums[i]+nums[j] == target {
                return []int{i, j}
            }
        }
    }
    return nil
}
```
>Golang練習，使用for迴圈的方式暴力解決

## 9. [Palindrome Number](https://leetcode.com/problems/palindrome-number/)[Easy]

Palindrome Number V1(反轉數字):
```
class Solution:
    def isPalindrome(self, x: int) -> bool:
        if( x < 0 or (x % 10 == 0 and x != 0)):
            return False

        rNum = 0
        while(x > rNum):
            rNum = rNum * 10 + x % 10
            x = x // 10

        return x == rNum or x == rNum // 10

```
>排除特殊情況後，把後半段反轉的數字錄入rNum來進行後續回文數的確認

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



# 課程內容 -- 其他

## BeautifulSoup - CNA新聞內容擷取

```
from urllib.request import Request, urlopen
from bs4 import BeautifulSoup
from google.colab import files
import time

url = 'https://www.cna.com.tw/'

headers = {'User-Agent': 'Mozilla/5.0 (Windows NT 10.0; Win64; x64)'}

req = Request(url, headers=headers)
html = urlopen(req).read().decode('utf-8')
soup = BeautifulSoup(html, 'html.parser')

news_links = [a['href'] for a in soup.find_all('a', href=True) if '/news/' in a['href']]

print(f"總共找到 {len(news_links)} 筆新聞連結")

all_news = ""

for i, link in enumerate(news_links, start=1):
    print(f"正在抓取第 {i} 篇新聞: {link}") 
    full_url = f'https://www.cna.com.tw{link}'
    
    req = Request(full_url, headers=headers)
    html = urlopen(req).read().decode('utf-8')
    soup = BeautifulSoup(html, 'html.parser')

    title = soup.find('h1').get_text(strip=True) if soup.find('h1') else '無標題'
    date = soup.find('div', class_='updatetime').get_text(strip=True) if soup.find('div', class_='updatetime') else '無時間'
    content = '\n'.join([p.get_text(strip=True) for p in soup.find('div', class_='paragraph').find_all('p')]) if soup.find('div', class_='paragraph') else '無內容'

    news = f"標題：{title}\n時間：{date}\n內容：\n{content}\n\n"
    all_news += news

    time.sleep(1)

with open('cna_news.txt', 'w', encoding='utf-8') as file:
    file.write(all_news)

files.download('cna_news.txt')

print("成功下載所有新聞檔案")
```
>擷取CNA新聞網中所有新聞的標題、時間、內容，並保存到txt檔中
