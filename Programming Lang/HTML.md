---
tags : web-develop
---

大標題
`<h1>TEXT<h1>`

比較小的標題
`<h2>TEXT<h2>`

段落
`<p>TEXT</p>`

註解
`<!--><-->`

## HTML5 elements
網頁的概要(顯示在搜尋引擎上)
```html
<main>
</main>
```

圖片(self-closing elements)
`alt` attribute用於圖片載入失敗時顯示
`target="_blank"`會開啟新分頁
`<img src="https://www.freecatphotoapp.com/your-image.jpg" alt="A business cat wearing a necktie." target="_blank">`

超鏈接(anchor)
`href` attribute代表鏈接的目的地
`<a href="https://freecodecamp.org">this links to freecodecamp.org</a>`

用超鏈接連到網頁內的section
```html
<h2 id="contacts-header">Contacts</h2>
...
<a href="#contacts-header">Contacts</a>
```

在paragraph內插入超鏈接
```html
<p>
 welcome to <a href="https://freecodecamp.org">codecamp</a>
</p>
```

### 超鏈接:dead link
`<a href="#" >cat photos</a>`

### 超鏈接+圖片
`  <a href="#"><img src="https://bit.ly/fcc-relaxing-cat" alt="A cute orange cat lying on its back."><a>`

### 清單: bulleted unordered list
`<ul>`list的起點
`<li>`list內的元素
	
```html
  <ul>
    <li>milk</li>
    <li>cheese</li>
    <li>me</li>
  </ul>
```

### 有序清單(ordered list)
```html
  <ol>
    <li>milk</li>
    <li>cheese</li>
    <li>me</li>
  </ol>
```

### 輸入欄位(self closing element)
`<input type="text">`
with placeholder
`<input type="text" placeholder="this is placeholder text">`
<input type="text" placeholder="this is placeholder text">
### 表格啦
> You can build web forms that actually submit data to a server using nothing more than pure HTML.

`<form action="/url-where-you-want-to-submit-form-data"></form>`

### 按鈕
> Clicking this button will send the data from your form to the URL you specified with your form's action attribute.

`<button type="submit">this button submits the form</button>`
<button type="submit">this button submits the form</button>

### 表格中的必填欄位
`<input type="text" required>`

### 單選按鈕(radio buttons)
* type of input
* 被包在`<label>`標籤內
* 每個按鈕都需要一個屬於他的label標籤
* for attribute會讓label匹配相同的input id
```html
	<label for="indoor"> 
  		<input id="indoor" type="radio" name="indoor-outdoor">Indoor 
	</label>
	<label for="outdoor"> 
  		<input id="outdoor" type="radio" name="indoor-outdoor">Outdoor 
	</label>
```
<label for="indoor"> 
	<input id="indoor" type="radio" name="indoor-outdoor">Indoor 
</label>
<label for="outdoor"> 
	<input id="outdoor" type="radio" name="indoor-outdoor">Outdoor 
</label>

### 多選按鈕(checkboxes)
一樣要被包在`<label>`內
```
    <label for="loving"><input id="loving" type="checkbox" name="personality"> Loving</label>
    <label for="simle"><input id="smile" type="checkbox" name="personality"> Smile</label>
      <label for="cute"><input id="cute" type="checkbox" name="personality"> Cute</label>
```
<label for="loving"><input id="loving" type="checkbox" name="personality"> Loving</label>
<label for="simle"><input id="smile" type="checkbox" name="personality"> Smile</label>
  <label for="cute"><input id="cute" type="checkbox" name="personality"> Cute</label>
	  
### 決定單選按鈕與多選按鈕的送出值
>When a form gets submitted, the data is sent to the server and includes entries for the options selected. Inputs of type radio and checkbox report their values from the value attribute.

```html
<label for="indoor"><input id="indoor" type="radio" name="indoor-outdoor"> Indoor</label>
```
當使用者選了indoor這個按鈕
form data會包含 `indoor-outdoor=indoor`(name與value attribute)
如果沒有填value欄位，預設是`indoor-outdoor=on`
不管選什麼都是這個，根本沒用

### 預設勾選
在input尾部加上`checked`
`<label for="indoor"><input id="indoor" type="radio" name="indoor-outdoor" value="indoor" checked> Indoor</label>`
<label for="indoor"><input id="indoor" type="radio" name="indoor-outdoor" value="indoor" checked> Indoor</label>

### 用`<div>`做分割
> The div element, also known as a division element, is a general purpose container for other elements.
>
> The div element is probably the most commonly used HTML element of all.
>
> Just like any other non-self-closing element, you can open a div element with <div> and close it on another line with </div>.

`<div></div>`

### 宣告doctype
提醒瀏覽器的資訊
> At the top of your document, you need to tell the browser which version of HTML your page is using. HTML is an evolving language, and is updated regularly. Most major browsers support the latest specification, which is HTML5. However, older web pages may use previous versions of the language.


```<!DOCTYPE html>
<html>

</html>
```

### 結構化: head & body
> Any markup with information about your page would go into the head tag. Then any markup with the content of the page (what displays for a user) would go into the body tag.
```
<html>
  <head>
  <title>The best page ever</title>
  </head>

  <body>
  <h1>The best page ever</h1>
  <p>Cat ipsum dolor sit amet.</p>
  </body>
</html>
```