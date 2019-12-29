# Question 1

The Dutch nationaal flag problem

一個陣列 A[M], A[M+1] ... A[N-1] 

裡頭每個元素都是紅、白、藍三色之一。

如何把它們由左至右依紅、白、藍的順序排好呢？

*Hint: think about the partition step in quick sort*

## Solution 1-1

利用O(n)的額外空間

建立3個list分別存A陣列裡的數值，

分為小於，等於，大於pivot

再回存list的值回A array

*時間複雜度: O(n)*

## Solution 1-2

透過swap element，

第一輪把比pivot小的值都移到A array的最前面

第二輪把比pivot大的值都移到A array的最後面


*空間複雜度: O(1)，只有要多增加swap的暫存空間*

*時間複雜度: 如果是使用雙層迴圈，O(n<sup>2</sup>)；如果使用另外紀錄交換位置的指標，O(n)*

## Solution 1-3

類似Solution 1-2，只是在一輪之內，就把大小分類好

> 在A array中，分成四類：小於pivot，等於pivot，未分類的，大於pivot，
剛開始所有的值都是在未分類中

**Example: **

A = [-3, 0, -1, **1, 1,** ?, ?, ?, 4, 2]

pivot = 1


要這樣分配的用意，在於要swap時會比較好換：

小於pivot：只要跟第一個1交換

等於pivot：不動

> 小於pivot：只要跟第一個1交換
等於pivot：不動
大於pivot：跟最後一個?(未分類)交換大於pivot：跟最後一個?(未分類)交換

*空間複雜度: O(1)，只有要多增加swap的暫存空間*

*時間複雜度: O(n)*


# Question 2

Increment an arbitrary-precision integer

有一個array D，請output D轉換成integer後，加一後的array

**Example: **

D = [1,2,9]

output = [1,3,0]

*Hint: 實際的例子*

## Solution 2-1

暴力法

轉換array to integer，加法運算後，再轉換回array

*但如果array超過integer的範圍，會overflow*

## Solution 2-2

利用數學加法的基本概念，一個位數一個位數相加，進位

*時間複雜度: O(n)，n為array D的長度*

# Question 3

Multiply two arbitrary-precision integers

計算兩個array的相乘結果，input及output皆為array

*Hint: 數學乘法的基本概念*

## Solution 3-1

暴力法

轉換array to integer，乘法運算後，再轉換回array

*但如果array超過integer的範圍，會overflow*

## Solution 3-2

利用數學乘法的基本概念

*時間複雜度: O(nm)，n m分別為兩個array的長度*

# Question 4

Advance through an array

從index 0 開始，array A的每個值代表最多可以走多少格，如果可以走到最後，return true

## Solution 4-1

直覺，greedy 每次都走最多步數

不是greedy的每次都走最多格就可以到終點

**Example: **

A = [2, 4, 1, 1, 0, 2, 3]，

如果都走最多步，2 -> 1 -> 1 -> 0 會走不到終點

但如果1 -> 4 -> 2 -> 終點

## Solution 4-2

紀錄最遠可以到哪裡

> 如果index < 最遠可到的地方，繼續計算
如果index > 最遠可到的地方，後面都到不了，不用計算
如果最遠可到的地方 > 最大index，可以到達終點，return true

*時間複雜度: O(n)*

# Question 5

Delete duplicates from a sorted array

sorted array A，移除掉裡面重複的值，回傳最後值的個數

*Hint: O(n) time, O(1) space solution*

## Solution 5-1

使用額外O(n)的空間

只要是新的值，存進額外的array中

*空間複雜度: O(n)*

## Solution 5-2

O(1) space 暴力法

只要發現值有重複，就把array後面的value都往前移

*空間複雜度: O(1)*

*時間複雜度: O(n<sup>2</sup>)*

## Solution 5-3

改進Solution 5-2

發現值有重複，不急著就把array後面的value都往前移

等到再次遇到新的值，再一併移動後面的value

*空間複雜度: O(1)*

*時間複雜度: O(n)*

# Question 6

Buy and sell a stock in once

一個array A，其值代表當日的某股票價格，如果只能一買後一賣，最大獲利為何

**Example: **

A = [310, 315, 275, 295, 260, 270, 290, 230, 255, 250]

max profit = 290 - 260 = 30

> 不一定買最底點，或是賣最高點，就會有最大的價差
不要找最高點跟最低點，因為最低點可能出現在最高之後

*Hint: valid difference*



