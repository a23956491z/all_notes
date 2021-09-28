---
tags : python
---

# Python基本語法整理
> **這是極淺而廣的Python教學筆記**

### 動態語言
> 指執行時可以改變其結構的語言
> 如變數參照型態的改變，函式、物件

^7a618b

### 直譯語言
> 編譯語言：寫完全部一次編譯給電腦執行
> 直譯語言：執行時一行行轉為機器碼

### python版本
> python2 和 python3有本質上的差異
> 不過許多套件都是以2版寫成，建議先學2版
> 且先學2版在學3版也不難轉換

### 安裝python
 * 先到官網下載并安裝
 * python預設被裝在 C:\Python版本 這個資料夾(如C:\Python27)
 * 將下列兩個路徑加入環境變數（以自己版本號套入）
 	1. C:\Python版本
 	2. C:\Python版本\Scripts
 * 進入cmd 輸入 `python --version`確認安裝

### python shell & python文件
 * 在terminal中(如cmd)鍵入 `python` 進入python shell
 * [https://docs.python.org/2/](https://docs.python.org/2/)  python完整文件

### 變數命名規則
 1. 以底線或英文字母開頭
 2. 名稱只可含以底線,英文字母和數字
 3. 不可與關鍵字相同
 4. 區分大小寫

### 變數參照
```python
>>> result = 2
```
> 以上是一個變數宣告或指定
> 事實上result沒有直接記錄 2
> 而是記錄了儲存 2 的空間
> 所以是可以轉換儲存形態的(轉換記錄空間)
> ```python
> >>> result = 2
> >>> result = 3.0
> >>> result = 'hello'
> >>> result = [1,2,3]
> ```
> 就像一個容器的***標籤***一樣

### 撰寫一個腳本
 * 通常以.py結尾
 * 以下是簡單的python程式碼(test.py)
```python
a = 10
b = 20
result = a + b
print result # result是30
```
 * `print`是印出資料， `#`後面代表的是註解
 * 接著只要在terminal中執行腳本
   而test.py是檔案名
   
```
python test.py
30
```

### 函式
> 就是封裝一套動作，供使用者**重複執行***
> * 使用函式 ```函式名(參數1,參數2,...)```
>   參數有幾個端看參數設計幾個參數給使用者使用
> * 不論有沒有設計參數，**小括號**都必須存在
> * 以下是使用函式的範例
> ```python
> print avg(1,2,3,4,5) #avg是內建的平均函式
> print abs(-10) #abs是內建的絕對值函式
> ```

### 資料型態
* 以下是整數運算的例子
```python
>>> 2 - 3
-1
>>> 2 * 3
6
>>> 6 / 4
1
>>> 6 % 4 #取餘數
2
>>> 2 ** 6 #次方
64
```

* 以下是浮點數運算的例子
```python
>>> 1.2 + 2
3.2
>>> 1.2e2 - 10 #1.2e2 即科學記號表示法表示120
110.0
>>> 3.2 / 1.1
2.909090909090909
>>> 4.2 % 3.2
1.0
```
* 布林數
> 只有真假值之分，如**`false`**,**`true`**

* 以下是字串的例子
```python
>>> string = ''
>>> string_a = 'h'
>>> string_b = 'ello'
>>> string_a + string_b
'hello'
```
字串不論使用 " 還是 ' 都可以
> * 還有特別的 文件字串可以保留格式，以一對 """
> ```python
> string_e = """
>     today is
>     a good day!
> """
> print string_e
> ```
> * 取出特定部分字串使用 [ ]
> ```python
> string = "hello world"
> print string[0] # 即第 0 個元素
> print string[0:5] # 即第 0 個到第 5 個元素
> ```
> **在電腦的世界中一切都是0開始**
>   而 上面的 0 即是 索引(index)
>   上面的 0:5 即是 切片(slicing)
>   
> * 指定切片時捨棄範圍
> ```python
> print string[:5] # 即第 0 個到第 5 個元素
> print string[6:] # 即第 6 個到最後一個
> print string[:] # 即全部
> ```
> * 填充字串，使用`format`方法以位置填充
> ```python
> string = 'My name is {0}, and i'm {1} years old'.format('Leo','10')
> ```
> * 以代名填充
> ```python
> string = 'Time is {time}'.format(time = '21:13')
> ```

### 跳脫字元
```python
>>> print '\thello world'
		hello world
>>> print 'hello\nworld'
hello
world
```

> 以下是一些跳脫字元
> 
> |跳脫字元|說明|
> |:-:| - |
> |\\|倒斜線|
> |\'|單引號|
> |\"|雙引號|
> |\n|換行|
> |\t|縮排|

### 使檔案支援中文
  在第一行加入 
  ```python
  # -*- coding: utf-8 -*-` 
  ```
  
### 群集物件
 * 清單 List
> 產生一個清單，以中括號包著
> ```python
> >>> lst = ['yoo', 100, 87.87] # 可以是不同型態
> ```
> 取出
> ```python
> >>> lst[0]
> yoo
> >>> lst[-1] # 即倒數第一個元素
> 87.87
> ```
> 取出子清單
> ```python
> >>> lst[:1]
> ['yoo',100]
> >>> lst
> ['yoo',100,87.87]
> ```
> 改變，刪除，及增加
> ```python
> >>> lst[0] = 123
> >>> lst.pop(1)
> >>> lst.append('wtf')
> >>> lst
> [123,87.87,'wtf']
> ```
 * 元組 Tuple
> 產生一個元組，以小括號包著
> **相對於清單，元組是不可變動的**
> ```python
> >>> tpl1 = (1, 2, 3)
> >>> tpl2 = (1,)
> ```
> **就算只有一個元素也要強制加上逗號**

 * 字典 Dictionary
> 一種應對型的資料結構，並不是純序列
> 每個位置含一個 **`key:value`**pair
> 以大括號包著
> 而前面做標籤的值為鍵(key)，不可變，後者反之
> ```python
> >>> dic = {'name' : 'Leo', 'age' = 16}
> >>> dic['name']
> Leo
> >>> dic['gender'] = 'male' # 自動加入
> >>> dic
> {'name' : 'Leo', 'age' : 16, 'gender' : 'male'}
> ```

### 巢狀結構
> ```python
> >>> person = ['Leo', 'Bill', ['duck', 17, 'male'] ]
> >>> person[2][1]
> 17
> ```
> ```python
> matrix = [ [1, 2, 3, 4],
> 			 [5, 6, 7, 8] ]
> print matrix[1][1] #結果是6
> ```

### 可變及不可變
> 改變變數時，變的是參照位址而非變數本身
> ```python
> a = 1
> a = 2 # 被改變的不是存放 1 的空間
> ```
> 相對的，字串本身也是不可變
> ```python
> a = 'hello'
> a[0] = 'b' #不合法
> TypeError
> ```

### 賦值運算
> **`= `**即是一個賦值運算子，將右側值給予左側
> ```python
> a = 10
> a = 20
> ```

### 空運算
> ```python
> pass # 代表什麼都不做
> ```

### 自身運算
> ```python
> a = 1
> a = a + 1 # 將 a + 1 給予左側變數
> a += 1 # 等價于上者
> ```

 常用**增強運算**表(若 a 預設 10 )
 
 | 運算子 | 範例 | 等價的自運算 | 結果 |
 |:-:|:-|:--|:--|
 | += | a += 5 | a = a + 5 | a 為 15 |
 | -= | a -= 5 | a = a - 5 | a 為 5 |
 | *= | a *= 5 | a = a * 5 | a 為 50 |
 | /= | a /= 5 | a = a / 5 | a 為 2 |
 | %= | a %= 5 | a = a % 5 | a 為 0 |
 | **=| a**= 5 | a = a** 5 | a 為 1e5|
 
### 比較運算
 | 運算子 | 說明 |
 | :-: | :-|
 | > | 左運算元是否大於右運算元 |
 | < | 左運算元是否小於右運算元 |
 | >= | 左運算元是否大於等於右運算元 |
 | <= | 左運算元是否小於等於右運算元 |
 | == | 左運算元是否等於右運算元 | 
 | != | 左運算元是不等於右運算元 | 
 
> 支援連續比較
> ```python
> >>> a = 5
> >>> 0 < a <= 5
> True
> ```
 
### 邏輯運算
> 主要有 **`and` `or ` `not`**三種
> ```python
> >>> True and Ture
> True
> >>> Ture and False
> False
> >>> False or False
> False
> >>> False or True
> True
> >>> not True
> False
> ```

### 身份運算
> **`is`**運算子判斷兩運算元是否來自同一記憶體位址
```python
>>> a = 1
>>> b = 1
>>> lst_1 = [1,2,3]
>>> lst_2 = [1,2,3]
>>> a == b
True
>>> a is b
True
>>> lst_1 == lst_2
True
>>> lst_1 is lst_2
False
```
> * 1 是屬於不可變資料
>   可以重複利用，python給予a b 相同的 1
> * 而清單是屬於可變資料
>   因為改變後會有不同結果
>   python給予不同的 [1,2,3]可變清單

### 隸屬運算
> **`in`** 判斷某資料是否為在另一資料之子集合
```python
>>> >>> lst = [1, 2, 3]
>>> a = 1
>>> a in lst
True
>>> 0 in lst
False
>>> string = 'hello world'
>>> 'hello' in string
True
```

### 條件運算
> 使用 **`if`**
> 如果月份介於三到五月即輸出
 ```python
if 3 <= month <= 5:
    print '現在是春季'
  ```
> <br\>
> 語法
```python
if 條件:
   區塊程式碼(suite)
```
> python中**0**,**None**,**空資料**(空字串,空清單等)都會被當做False
> <br\>
> 而程式碼區塊以**縮排**表示
``` python
if 3 <= month <= 5:
    print '現在是春季'
    print '一年之計在於春'
print '這裡不屬於if區塊'
```
> <br\>
> 以**`else`**執行如果為否
```python
if 3 <= month <= 5:
    print '現在是春季'
else:
    print '現在不是春季'
```
> <br\>
> if/else算式
> ```python
> string = '現在是春季' if 3 <= month <= 5 else '現在不是春季'
> # 如果條件成立即返回前者，不成立反之
> ```
> <br\>
> **`elif`**否則如果
```python
if 3 <= month <= 5:
    print '現在是春季'
elif 6 <= month <= 8:
    print '現在是夏季'
elif 9 <= month <= 11:
    print '現在是秋季'
else:
    print '現在是冬季'
```

### while迴圈
> **`while`**關鍵字
```python
_sum = 0
num = 1
while num < 11: #while後條件成立即重複執行
    _sum += num
    num += 1
```

### break與continue
* **`break`**中斷迴圈敘述，直接跳出
```python
n = 5
count = 1
while True: # 無窮迴圈
    print 'just print {n} times'.format(n=n)
    if count == n:
        break
    count += 1
```
* **`continue`** 略過某一次結果
```python
num = 1
while num < 11:
    if num==5:
        num += 1
        continue
    print num
    num += 1
```

### for迴圈
> 迭代重複執行
* **`for`** item **`in `**list
  將list元素一一取出賦予item，并執行一次for區塊
```python
  lst = [1, 3, 6]
for num in lst:
    print num
```

### Comprehension (含內迴圈)
> 在建造清單，字典時搭配迴圈
```python
lst = [1, 2, 3, 4, 5]
lst_sq = [] 
for num in lst:
    lst_sq.append(num**2) # 每個元素平方後放入
```
> 而上述迴圈等價於以下comprehension
```python
lst = [1, 2, 3, 4, 5]
lst_sq = [num ** 2 for num in lst]
```
> 甚至加入條件判斷
```python
lst = [1, 2, 3, 4, 5]
lst_sq = [num ** 2 for num in lst if num % 2 == 0]
```
> <br\>
> 字典配上comprehension
```python
scores = [88, 90, 100, 65, 78]
score_dic = { student_id:score for student_id, score in enumerate(scores)}
```
> * stuednt_id:score 即**`key:value`** pair的格式
> * **`enumerate()`**是一函數，會返回元素與其位置的**`key:value`**pair

### 基本輸入輸出
* 使用逗號單次輸出**多筆不換行**資料
```python
>>> print 1,2,3
1 2 3
```
* print預設多次輸出自動換行
```python
print 1
print 2
print 3
# 結果將會分三行
```
* print使用逗號多此輸出不斷行列印
```python
a, b = (1, 2)
print a,
print b
# 結果只會有一行
```
* 使用**`input`**進行輸入
  以下是一個簡單的猜數字
```python
answer = 6
while True:
    str_num = input('請輸入一個1-10之間的整數:')
    int_num = int(str_num)
    if int_num == answer:
        print('猜中拉！')
        break
```
> **`input()`**內的字串提供使用者輸入提示
> **`input()`**將輸出結果返回 **`str_num`**
> 而返回結果是字串，若要與整數進行比較需要轉型
> **`int()`**可以把資料轉成整數型態

>可能的輸出結果
```python
請輸入一個1-10之間的整數:9
請輸入一個1-10之間的整數:1
請輸入一個1-10之間的整數:4
請輸入一個1-10之間的整數:6
猜中拉！
```

### 檔案的輸入輸出(跳過)

### 例外與捕捉(跳過)

### 函式
* 工廠函式(負責製造資料或轉型的函式)
> **`int()`**就是一種
```python
string = '100'
a = int(string)
``` 
* 常見工廠函式

| 內建函式 | 敘述 |
| :-: | :- |
|int|製造整數或將其他型態資料轉為整數 |
|float|製造浮點數或將其他型態資料轉為浮點數|
|bool|製造布林值或是將其他型態資料轉為布林值|
|str|製造字串或是將其他型態資料轉為字串|
|list|製造清單或是將其他型態資料轉為清單|
|set|製造集合或是將其他型態資料轉為集合|

> set(集合)類似一種無重複資料的清單
* "全部或任何"內建函式
> **`all()`**只要清單內全都為真，返回真
> **`any()反之`**
```python
pass_data = [True, True, True, False, False]
if all(pass_data):
    print '都及格了，歐啪'
elif any(pass_data):
	print '至少一個及格'
else:
    print '有人不及格'
```
* "最大與最小"內建函式
```python
lst = [1,2,3,4,5]
print max(lst)
print min(lst)
```

* "產生連讀的整數"內建函式
```python
for num in range(10):
	print num
```
> **`range(X)`**會產生0 ~ (x-1)的整數序列

```python
for num in range(2, 6): # 產生 2 ~ 6
	print num
```
* "群集長度"內建函式
```python
lst = [1, 2, 3, 4, 5]
print len(lst) # 返回 5
dic = {1:1, 2:2, 3:4} 
print len(dic) # 返回 3
```

### 自定義函式
* 使用**`def`**做開頭，且函式內會有一個回傳值
```python
def add(a, b):
    return a + b
print add(1,2) # print 3
```
* 格式
```python
def 函式名稱(參數1, 參數2, ...):
    若干運算(敘述)
    return 回傳值1, 回傳值2 ...
```
> 而參數**可有可無**
> 而返回值同樣也是，甚至可以回傳多個
* 呼叫
```python
def power(base, exp):
    return base ** exp
print power(2, 3)
print add(base = 2, exp = 3) # 關鍵字呼叫
print add(exp = 3, base = 2) # 關鍵字呼叫
# 以上三者呼叫等價
```
> 使用關鍵字呼叫即可以不需要知道參數的確切順序

* 遞迴
> 重複執行函式自身的演算法

> 假如有一巢狀清單，而我們不知其層數
> 欲把"每個元素"都印出來
```python
for item in lst:
    if isinstance(item, list):
        for item2 in item:
            print item2
    else:
        print item
```
> **`ininstance(data, type)`**判斷data是否為type型態
> 此方法看似可行，卻只能解二階清單，不符合我們的要求
```python
def print_list(lst):
    for item in lst:
        if isinstance(item, list):
            print_list(item) # 執行函式自身(再進入一個list)
        else:
            print item
```
> 不論位於那一層，只要發現list則進入之
> 如剝洋蔥一樣，不需煩惱要剝幾層

* 參數的預設值
> 呼叫函式值不必提供相同數量的參數
    ```python
    def add(a, b = 1): 
        return a + b
    print add(1,2)
    print add(1)
    ```
> 如果不提供參數 b 則會使用預設值 1 
> **而預設參數後面不可有非預設參數**

* 使用綴星運算子把list unpack當參數

	```python
	def add(a,b,c,d):
	    return a+b+c+d

	lst = [1,2,3,4]
	print add(*lst) # 使用 '*' unpack
	```
> **`*lst`**會執行拆解的動作把 lst 拆成 1,2,3,4

* 在參數使用 unpack

	```python
    def add(*lst): # 允許 N 個資料輸入
    	return sum(lst)
    
    print add(1, 2)
    print add(1, 2, 3, 4)
    ```
    
* 對字典 unpack
> 使用 雙星號 `**` ，把字典拆解成好幾個 value 捨棄key

	```python
    def power(base, exp):
    	return base ** exp
    
    dic = {'base' = 2, 'exp' = 3}
    print power(**dic) # print power(2, 3)
	```
    
### 變數的有效範圍
* 全域變數
	*  定義在函式外的變數其範圍是一整個檔案
* 區域變數
	*  定義在函式中的變數其範圍是一整個函式
* 而內部變數會**遮蔽**外部變數

	```python
	def test_scope():
	    var1 = 1
 	   print var1, var2

	var1 = 0
	var2 = 0

	test_scope()
	print var1, var2
	```   
> 輸出

	```python
    1 0
    0 0
    ```
    
### 閉包與裝飾器
> 以函式包裹函式，參照外部環境的函式


```python
def gen_power(base):
    def power(exp):
        return base ** exp
    return power

power2 = gen_power(2)
power3 = gen_power(3)

print power2(3) # 2 ** 3
print power3(2) # 3 ** 2
```
> power 參照了外部的函式 base 變數
> 這就是一種閉包(power函式)

> 裝飾器：藉閉包產生修飾其他函式的函式

<br>
* 使用一個裝飾器
   裝飾器以 **`@`**開頭，後面緊接著要修飾的函式

```python
@print_result # 使函式print結果
def add(*lst):
    return sum(lst)

@print_result
def power(base,exp):
    return base ** exp

add(1,2,3,4,5) # 自動print
power(2,3) # 自動print
```
> 也可以使用閉包的格式

```python
def add(*lst):
	return sum(lst)
add = print_result(add)
```

* 撰寫裝飾器

```python
def print_result(func):
    def modified_func(*args,**kwargs):
        print func(*args,**kwargs)
    return modified_func
```
> 透過綴星運算式，可以接受任意數量的位置引數和關鍵字引數
> 就是上述的 `*args` , `**kwargs`

* 使裝飾器接受參數
> 例如下效果

```python
@print_result(head='result:')
def add(*lst):
    return sum(lst)

add(1,2,3,4,5)

---(結果)---
result: 15
```
> 而使用裝飾器部分等價於

```python
add = print_result(head='result:')(add)
```
> 簡而言之，裝飾器接受func本身作為引數
> 所以必須在裝飾器外再額外寫一個接受參數的函式

```python
def print_result(head):
    def decorater(func):
        def modified_func(*args,**kwargs):
            result = func(*args,**kwargs)
            print head, result
        return modified_func
    return decorater
```

### 物件
> 類別(class)就是資料的型態
> 而物件即是類別實際的例子(instance)
> 例如整數1，字串'hello world'，甚至函式也是物件

### 封裝
> 把屬性封在類別中，也就是資訊隱藏
> 例如類別屬性只給同類別方法使用
* 變數前加上 **`__`** 限定物件只可在類別內存取

```python
class someData:
	def __init__(self, num):
    	self.a = num
    
    def return_a(): # 要取得 a 要透過函式
    	return self.__a
        
    def set_a(num): # 要更改 a 也是
		self.__a = num
```

### 自定義類別
```python
class Cat:
    def __init__(self, name):
        self.name = name
    def shout(self):
        print 'Meow'
```
> **`class`** 是定義類別的關鍵字
> 通常以 **`__init__`** 作為第一個函式
> 每個函式必定以 **`self`**作為第一個參數
>  * **`self.name `**即是一個屬性
>  * **`__init__`** 即建構方法
>    當產生一個物件時會先呼叫他

* 生成一個Cat物件
```python
my_cat = Cat('Kitty')
== 其真正樣貌 ==
Cat.__init__(my_cat,'Kitty')
```
> 而'Kitty'即對應 **`__init__`**中的name參數
> self即是"物件"本身的意思

### 繼承
> 剛剛我們有了貓這個類別
> 如果我們還要新增行為及屬性幾乎相同的狗類別，不就需要重寫嗎？
> 這時可以創造一個animal類別，讓貓狗繼承之

```python
class Animal:
    def __init__(self, name):
        self.name = name
    def run(self):
        print self.name, 'runs'
    def jump(self):
        print self.name, 'jumps'

class Cat(Animal):
    def shout(self): # 原本沒有的
        print 'Meow'
        
class Dog(Animal):
    def shout(self):
        print 'Bark'
```
> 小括號內的類別即我們要繼承的類別(父類別)
> 而繼承後可以自行加上原先沒有的，或更改原先有的

```python
class Human(Animal):
    def __init__(self, name, id): # 覆寫原本就有的
        self.name = name
        self.id = id   
```

### Tkinter寫GUI
* 首先要先匯入模組
```python
import Tkinter
```

* 呼叫**`Tk()`**建立視窗實體
```python
import Tkinter
win = Tkinter.Tk()
```
> 用別名的方式呼叫Tkinter函式

    ```python
    import Tkinter as tk
    win = tk.Tk()
    ```
> 甚至匯入所有Tkinter函式的方式使用Tkinter

    ```python
    from Tkinter import *
    win = Tk() # 不用指定類別名
    ```
> 缺點是佔用記憶體，命名空間混淆，難以debug

* 使用新版 ttk
> 界面會比較漂亮
> 使用方法完全一樣，只是匯入方式不太相同

    ```python
    from Tkinter import ttk
    win = ttk.Tk()
    ```
>或

    ```python
    from ttk import *
    win = Tk()
    ```

* 加入事件監視迴圈(執行GUI)
```python
win.mainloop()
```
* 設定視窗屬性
```python
win.title("My First GUI") # 視窗標題命名為"My First GUI"
```
![改視窗標題](https://1.bp.blogspot.com/-T2TRCKt9tgc/Vz6EBFgCPUI/AAAAAAAAFwo/hl_AKkmWVcM9iPfqeR5_Xs9_zLc4hSkKACLcB/s1600/Tkinter_%25E8%25A6%2596%25E7%25AA%2597%25E6%25A8%2599%25E9%25A1%258C.jpg)

* Tkinter 元件
    1.     Label
    1.     Button
    1.     Radiobutton
    1.     Checkbutton
    1.     Entry
    1.     Frame
    1.     LabelFrame
    1.     Listbox
    1.     Text
    1.     Message
    1.     PanedWindow
    1.     Scrollbar
    1.     Scale
    1.     Spinbox
    1.     Menu
    1.     OptionMenu
    1.     Menubutton
    1.     Canvas
    1.     Image
    1.     Bitmap
    1.     Toplevel

* ttk的額外元件
    1. Combobox
    1. Notebook
    1. Progressbar
    1. Separator
    1. Sizegrip
    1. Treeview



* 試用 Button & Label 元件
	* 第一個參數必須為**容器**
	* 其他參數為元件屬性如 text, size, border..
	* 而元件要顯示需利用**版面管理員**
	  而**`.pack()`**就是一個檔案管理員
      他將**由上而下**的擺放元件
      
    * 也可以使用字典的方式設定屬性


```python
import Tkinter as tk

win=tk.Tk()     
win.title("Tk GUI")

label=tk.Label(win, text="Hello World!") 
button=tk.Button(win)
button["text"] = "ok" # 以使用字典的方式

label.pack()
button.pack()    
win.mainloop()
```

* **`.grid()`**版面管理員

```python
from Tkinter import *

win=Tk()
win.title("Tk GUI")

label=Label(win, text="Hello World!")
button=Button(win, text="OK")

label.grid(column=0,row=0)
button.grid(column=1,row=0)
win.mainloop() 
```




