# Question 1
Computing the parity of a binary word

計算binary word中1出現個個數，如果是奇數，擇他的parity是1，反之是0


*Hint: 考慮64-bit word的情形*

## Solution 1-1
shift word並 AND mask 1


*時間複雜度: O(n)*

## Solution 1-2
每次都drop word中最小(最右邊)的bit 1，看drop幾次

> 只取最小的bit 1: x & ~(x-1) 
丟棄最小的bit 1: x & (x-1) 


**Example:**

x:              11010

x-1:           11001

~(x-1):       00110

x & ~(x-1): 00010

x &  (x-1):  11000


*時間複雜度: O(k), k是word中bit 1的個數*

## Solution 1-3
使用cache table，查表

word 長度為64-bit，cache table可以為16-bit

利用shift 和 0xffff mask 16個bit為一組去查表，再把結果XOR起來


*時間複雜度: O(n/L)，n是word長度，L是cache長度*

## Solution 1-4
利用XOR的特性

//TODO


# Question 2
Swap Bits

有一個64-bit的integer，指定 i 和 j 兩個位置的bit，並互換其值，來得到新的int


*Hint: 真的需要互換嗎？*

## Solution 2-1
暴力法

利用mask，得到 i 和 j 位置的bit，分別存下來並互換，再利用bitwise operation改其值

## Solution 2-2
不用真的swap，因為bit的值只有0和1

看看 i j 兩個位置的bit一不一樣，相同代表互換沒差，結果還是原本的integer，不相同才需要繼續處理


> 因為XOR的特性，
0^1 = 1，
1^1 = 0，
和1做XOR，得到的bit會相反
而和0做XOR，可以保留原本的bit


利用只有 i j 位置是1的mask(e.g. 0001000100) XOR integer


*時間複雜度: O(1)，看word有多長*


# Question 6
Compute x/y

假設x, y皆為正整數，利用addition, subtraction shifting operation 計算x/y


*Hint: x/y --> (x-y)/y*

## Solution 6-1
暴力法

重複x-y，直到x<y


*時間複雜度: 但當x, y 相差很多時，會需要執行很多次
(e.g. x = 2 <sup>31</sup> , y = 1，要執行 2 <sup>31</sup> -1次)*

## Solution 6-2
優化x-y的過程，不要一次只減一個y

> 找到 2<sup>k</sup>y <= x，最大的k


**Example:**

x: (1011)<sub>2</sub> 

y: (10)<sub>2</sub>

k: 2

step 1: 
x - 2<sup>2</sup>y = (1011)<sub>2</sub> - 2<sup>2</sup>(10)<sub>2</sub>, 

remainder: x = (11)<sub>2</sub>, 

quotient: 1 x 2<sup>k</sup> = 1 x 2<sup>2</sup> = (100)<sub>2</sub>


step 2:
x - 2<sup>0</sup>y = (11)<sub>2</sub> - 2<sup>0</sup>(10), 

remainder: x = (1)<sub>2</sub>,  (x < y 不用再執行loop)

quotient: quotient + 1 x 2<sup>0</sup> = (100)<sub>2</sub> + (1)<sub>2</sub> = (101)<sub>2</sub> 


*時間複雜度: O(n)*


# Question 7
Compute a<sup>b</sup>

假設a是double，b是integer


*Hint: 指數的特性*

## Solution 7-1
暴力法

a<sup>2</sup> = a x a

a<sup>3</sup> = a<sup>2</sup> x a

... 要計算b-1次


時間複雜度: O(2<sup>n</sup>)

## Solution 7-2
一次不止乘上一個a，減少相乘次數

**Example: **

1.1<sup>20</sup>  = 1.21<sup>10</sup>


> 如果b的least significant bit = 0，可以把a拆成(a<sup>2</sup>)<sup>y/2</sup>，也就是a<sup>y/2</sup> x a<sup>y/2</sup>
如果b的least significant bit = 1，可以把a拆成a x (a<sup>2</sup>)<sup>y/2</sup>


**Example:**

a<sup>(1010)<sub>2</sub></sup> = a<sup>(101)<sub>2</sub></sup> x  a<sup>(101)<sub>2</sub></sup>,

a<sup>(101)<sub>2</sub></sup> = a x a<sup>(100)<sub>2</sub></sup> = a x a<sup>(10)<sub>2</sub></sup> x a<sup>(10)<sub>2</sub></sup>


時間複雜度: O(n)，at most twice the index of most significant bit 

# Question 8
reverse digits

假設x是integer 123，回傳321，如果是-123，則回傳-321


Hint: 如果是reverse string, how to solve?

## Solution 8-1
暴力法

轉換intger to string，traverse te string from back to front

## Solution 8-2
不用轉換為string，透過modulo 10取最小位數

時間複雜度: O(n)，n是digit個數

# Question 9
Check if a decimal integer x is a palindrome

符合，e.g. 0, 1, 7, 121, 333, 123321...

不符合，e.g. -1, 12, 100...

*Hint: 找到least significant digit很容易，但如何找到most significant digit?*


## Solution 9-1
暴力法

轉換intger to string，依序比較最小及最大digit相不相同，一旦發現不同就回傳false

時間複雜度: O(n)，n是digit個數

## Solution 9-2
不轉換為string，找到number中的most significant digit

而most significant digit n = floor(log<sub>10</sub>x) + 1

**Example: **

100的most significant digit = floor(log<sub>10</sub>100) + 1 = 2 + 1 = 3

> least significant digit: x mod 10
most significant digit: x/10<sup>n-1</sup>

*時間複雜度: O(n)
空間複雜度: O(1)*


# Question 10
Generate uniform random numbers

現有一個公平挑出0 和 1 的generator ，利用它製造出一個generator可以在integer a 跟 b 之間公平的挑出integer i

## Solution 10-1
把現有一個公平挑出0 和 1 的generator想像成一個bit

看要處理的範圍 b - a，至少需要用多少個bit來表示

Example:

直骰子，1~6 隨機挑出一個數字

2<sup>2</sup>-1 < 6-1 <= 2<sup>3</sup>-1

所以至少需要3個bit來表示所有數字，分別是

(000)<sub>2</sub>, (001)<sub>2</sub>, (010)<sub>2</sub>, (011)<sub>2</sub>, (100)<sub>2</sub>, (101)<sub>2</sub>

如果random數字是(111)<sub>2</sub>, (110)<sub>2</sub>，則每個bit再重新random一次

*時間複雜度: *

# Question 11
Rectangle intersection

在一個x-y二為的座標系中，有若干個長方形，且邊都平行於座標軸

試問某兩個長方形R<sub>1</sub>和R<sub>2</sub>是否有相交，回傳相交的範圍

(只要有共同邊，共同頂點，也算相交)

*Hint: x, y座標分別處理*

## Solution 11-1

相交的情形有很多種，反向思考，兩個長方形是否不相交？

> 分別看x, y 軸，
chek if 
R<sub>1</sub>的左下角頂點座標 + R<sub>1</sub> x軸邊長後 >＝ R<sub>2</sub>的左下角頂點座標 
且
R<sub>2</sub>的左下角頂點座標 + R<sub>2</sub> x軸邊長後 >＝ R<sub>1</sub>的左下角頂點座標 

*時間複雜度: O(n)*


