---
tags : python
---


[![hackmd-github-sync-badge](https://hackmd.io/OXaFMlr_RbyVfBcbLHlfCQ/badge)](https://hackmd.io/OXaFMlr_RbyVfBcbLHlfCQ)

以下兩種皆可：
 1.  python.requests
 2. selenium.webdriver

## selenium.webdriver
先跳過

## requests
安裝  ` > pip install requests `


### `GET`請求
直接下載單純的網頁
```python
# 引入 requests 模組
import requests

# 使用 GET 方式下載普通網頁
r = requests.get('https://www.google.com.tw/')
```
變數`r`接受伺服器傳回的資料
```python
# 伺服器回應的狀態碼
print(r.status_code)
```
>
顯示`200`代表沒問題
也可以使用內建常數做判斷
```python
# 檢查狀態碼是否 OK
if r.status_code == requests.codes.ok:
  print("OK")
```
<br/> <!-- >換行<-->

### 取得HTML原始碼
可以從`r.text`取得
```python
# 輸出網頁 HTML 原始碼
print(r.text)
```

### 增加 URL 查詢參數
```python
# 查詢參數
my_params = {'key1': 'value1', 'key2': 'value2'}

# 將查詢參數加入 GET 請求中
r = requests.get('http://httpbin.org/get', params = my_params)
```
我們可以觀察最後所產生的 URL：
```python
# 觀察 URL
print(r.url)
```
>http://httpbin.org/get?key2=value2&key1=value1
---
### 其他資料
#### 帳號密碼登入

若遇到需要帳號與密碼登入後才能看的網頁（[HTTP 基本認證](https://zh.wikipedia.org/wiki/HTTP%E5%9F%BA%E6%9C%AC%E8%AE%A4%E8%AF%81)），可以使用  `auth`  參數指定帳號與密碼：
```python
# 需要帳號登入的網頁
r = requests.get('https://api.github.com/user', auth=('user', 'pass'))
```
#### `POST`  請求

`POST`  請求也是很常用的 HTTP 請求，只要是網頁中有讓使用者填入資料的表單，大部分都會需要用  `POST`  請求來處理，以下是一個簡單的範例：
```python
# 資料
my_data = {'key1': 'value1', 'key2': 'value2'}

# 將資料加入 POST 請求中
r = requests.post('http://httpbin.org/post', data = my_data)
```
若有遇到重複鍵值（key）的 HTML 表單欄位，可以這樣處理：
```python
# 具有重複鍵值的資料
my_data = (('key1', 'value1'), ('key1', 'value2'))

# 將資料加入 POST 請求中
r = requests.post('http://httpbin.org/post', data = my_data)
```
#### 上傳檔案

若要上傳檔案，也可以使用  `POST`  請求來處理，這是一個上傳 Word 文件的範例：
```python
# 要上傳的檔案
my_files = {'my_filename': open('my_file.docx', 'rb')}

# 將檔案加入 POST 請求中
r = requests.post('http://httpbin.org/post', files = my_files)
```
#### 等待逾時

`requests`  預設會一直等待直到伺服器完成回應為止，如果想改變等待逾時設定，可以用  `timeout`  設定（單位為秒）：
```python
# 等待 3 秒無回應則放棄
requests.get('http://github.com/', timeout = 3)
```
等待逾時設定是指伺服器無回應的狀態下所等待的時間，更精確的說就是完全沒有收到任何資料的狀況下，可等待的最常時間。

#### 不合格憑證

當我們在自架網頁伺服器進行測試時，HTTPS 時常會有憑證不合格的問題，當  `requests`  遇到這種伺服器就容易會出現  `requests.exceptions.SSLError`  這樣的錯誤，解決的方式就是加上  `verify=False`，關閉  `requests`  的憑證檢查功能：
```python
# 關閉憑證檢查
r = requests.get('https://my.server.com/', verify = False)
```

---

# 分析資料
以下兩種皆可
1. beautifulsoup
2. json

## Json
先跳過

## BeautifulSoup

### 網頁簡介
首先網頁內容大致可以分成**HTML語法**、**CSS網頁樣式**以及**javascript**這三類。
**網頁的資料就是由各式標籤 (tag) 所組成的階層式文件，要取得所需的網頁區塊資料，只要用 tag 與相關屬性去定位資料所在位置即可**。

例如這個網頁：
![](https://raw.githubusercontent.com/jwlin/jwlin.github.io/master/images/161222-python-ds-tutorial-3-1.png)

```html
<html>
  <head>
    <title>我是網頁標題</title>
    <style>
    .large {
      color:blue;
      text-align: center;
    }
    </style>
  </head>
  <body>
    <h1 class="large">我是變色且置中的抬頭</h1>
    <p id="p1">我是段落一</p>
    <p id="p2" style="">我是段落二</p>
    <div><a href='http://blog.castman.net' style="font-size:200%;">我是放大的超連結</a></div>
  </body>
</html>
```

>HTML 文件內不同的標籤 (例如 \<title\>, \<h1\>, \<p\>, \<a\> 有著不同的語義，表示建構網頁用的不同元件，且標籤可以有各種屬性 (例如 id, class, style 等通用屬性, 或 href 等專屬屬性)，因此我們可以用標籤 + 屬性去定位資料所在的區塊並取得資料。關於網頁架構還有另外一件事，就是它是階層式文件，例如以上的網頁架構可以如下表示：


![2016-12-22-2](https://raw.githubusercontent.com/jwlin/jwlin.github.io/master/images/161222-python-ds-tutorial-3-2.png)

## 用法
### selenium:
```python
from selenium import webdriver
browser = webdriver.Chrome(executable_path=driverPath)
browser.get('URL')
```

```python
tab = browser.find_element_by_id('Tab'+ str(color))

```
```python
from skimage import io
option = browser.find_element_by_xpath("//select[@id='selectday']/option[text()='{}']")
img = browser.find_element_by_xpath('//img[@data-elem="pinchzoomer"]')
src = img.get_attribute('src')
axs.imshow(io.imread(src))
area = area_input.find_element_by_xpath('..')
```

### beautiful soup
```python
import requests
from bs4 import BeautifulSoup

html = requests.get('url')
html.encoding = 'utf8'
sp = BeautifulSoup(html.text, 'html.parser')
```
```python
table = sp.find(id='BodyContent_gvActs')
tr_list = table.find_all('tr', recursive=False)
lst.append(td_list[4].find('span').text)
```

### Pandas 

### MatPlotLib
```python
import matplotlib.pyplot as plt
plt.rcParams['font.family'] = 'Microsoft JhengHei'
plt.figure(figsize=(16,12))
plt.subplot(221)

axes = plt.gca()
axes.set_ylim([0,40])

plt.yticks(np.arange(0, 41, step=5))
plt.bar(data.keys(), data.values())

plt.subplot(222)
y_pos = np.arange(len(data.keys()))
plt.barh(y_pos,  data.values(), align='center')
plt.yticks(y_pos, data.keys())
plt.gca().invert_yaxis()
plt.xticks(np.arange(0, 41, step=5))

plt.subplot(223)
plt.plot(data.keys(), data.values())
plt.yticks(np.arange(0, 41, step=5))

plt.subplot(224)
plt.pie(data.values(),
        labels=data.keys())

Path("images").mkdir(parents=True, exist_ok=True)
plt.savefig('images/410821238_3-1.jpg', bbox_inches='tight')
plt.show()
```

```python
df = pd.DataFrame(data)
df = df.set_index('年資學歷')
df = df.reindex(index=df.index[::-1])

plt.figure(figsize=(10,8))
plt.rcParams['font.family'] = 'Microsoft JhengHei'

for c in df.columns:
    plt.plot(df.index, df[c], label=c)

plt.axis((0,10,20000,50000))
plt.yticks(np.arange(20000, 50001, step=5000))
plt.legend()
```

### Datetime
```python
import datetime
datetime.datetime.strptime(time, '%Y/%m/%d %H:%M')
time_str = date.strftime("%Y/%m/%d %H:%M")
datetime_input -= datetime.timedelta(minutes=10)
# days, seconds, microseconds=, milliseconds=0, minutes=0, hours=0, weeks=0
```