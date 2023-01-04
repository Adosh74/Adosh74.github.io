#codeforces

### A. Soldier and Bananas
 - w number of bananas  want to buy
 - k  number of dollars for first banana and 2k for second and so on
 - n dollars he has
 - input (k, n, w)
 - No. output dollars should borrow to get w

    code: : 💻
```    
k, n, w = list(map(int, input().split()))

totalCost = 0

for i in range(1, (w+1)):
	totalCost += (k * i)

borrow = totalCost - n

if borrow < 0:
	print(0)
else:
	print(borrow)
```


 ###  617A - Elephant 
	
   - code: : 💻
    
    
                  
           from math import ceil

          x = int(input())

          steps = (x / 5)

          if ceil(steps) == steps and steps != 0:
              print(int(steps))
          else:
              print(int(steps+1))
         
         
###  59A - Word 

   code: 💻
```
s = input()

countUp = 0
countLow = 0

for i in range(0, len(s)):
	if s[i].isupper():
		countUp += 1
	else:
		countLow += 1

if countUp > countLow:
	print(s.upper())
else:
	print(s.lower())
```
    
### A. Wrong Subtraction


code: : 💻

```
n, k = list(map(int, input().split()))

for i in range(k):
    if n % 10 == 0:
        n = n / 10
    else:
        n = n - 1

print(int(n))
```
