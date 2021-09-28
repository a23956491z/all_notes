#web-develop

Cascading Style Sheets (CSS) tell browser **how to display**the text the other content that you write in HTML.

CSS has been adopted by all major browsers and allows you to control:
* color
* fonts
* positioning
* spacing
* sizing
* decorations
* transitions

> The idea behind CSS is that you can use a selector to target an HTML element in the DOM (Document Object Model) and then apply a variety of attributes to that element to change the way it is displayed on the page.

### Color of Text
> 在style的結尾加上`;`是個好習慣

注意：這個用法是inline style
`<h2 style="color: blue;">CatPhotoApp</h2>`
<h2 style="color: blue;">CatPhotoApp</h2>

### CSS Selector
用inline style我們儘改變單一個標籤
然而我們可以使用selector一次改變多個標籤
在`<style>`標籤內使用selector

這個寫法會把所有`<h2>`標籤的style都改掉
```html
<style>
	h2{
		color: red;
	}
</style>
```

也可以宣告CSS class重複使用style
記得要指定標籤的class atrribute
```html
<style>
  .blue-text {
    color: blue;
  }
</style>
...
<h2 class="red-test">CatPhotoApp</h2>
```

### Font Size
```html
<style>
  p{
    font-size: 16px;
  }

</style>
```

### Set Font Family
Font family的格式是`font-family: FAMILY_NAME, GENERIC_NAME;`
而`GENERIC_NAME`非必要，當前者不可用時會替補

```html
h2 {
  font-family: sans-serif;
}
```

Google fonts library
```html
<link href="https://fonts.googleapis.com/css?family=Lobster" rel="stylesheet" type="text/css">
<style>
  p {
    font-family: Lobster;
  }
</style>
```

如果Font的名字有空格，要記得加上雙引號
如`"Open Sans"`

預設的字型：
* `monospace`
* `serif`
* `sans-serif`

### Resize Image
```css
  .smaller-image{
    width: 100px;
  }
```

### Border
border有以下屬性
* `style`
* `color`
* `width`
```css
  .thin-red-border {
    border-color: red;
    border-width: 5px;
    border-style: solid;
  }
```

標籤使用多個style class時要加空格
`<img class="class1 class2">`

可以藉由`border-radius`加上圓角
```css
  .thick-green-border {
    border-color: green;
    border-width: 10px;
    border-style: solid;
    border-radius: 10px;
  }
```
甚至是把圖片變圓形的
`border-radius: 50%;`

### Font background color
```css
  .silver-background {
  background-color: silver;
}

  body {
    background-color: #000000;
  }
  body {
    background-color: rgb(0, 0, 0);
  }
  
  .cyan-text {
    color: #0FF;
  }
```


### 藉由id指定element的style
注意：`id`不可重複使用
且相較於class有更高的style優先度

`#cat-photo-form`藉由井號select元素
```css
  #cat-photo-form{
    background-color: green;
  }
```

### Padding&Margin
每個HTML元素附近都被`padding`，`border`，`margin`環繞著
* `padding`控制內容與`border`的距離(space)

```css
  .blue-box {
    background-color: blue;
    color: #fff;
    padding: 20px;
  }
```

* `margin`控制元素`border`與其他元素的距離
```css
  .red-box {
    background-color: crimson;
    color: #fff;
    padding: 20px;
    margin: -15px;
  }
```
   而`margin`的值若是負的，則該元素會比預設再大些

還可以指定不同方向的padding
```css
  .blue-box {
    background-color: blue;
    color: #fff;
    padding-top: 40px;
    padding-right: 20px;
    padding-bottom: 20px;
    padding-left: 40px;
  }
```

不同方向的margin
```css
  .blue-box {
    background-color: blue;
    color: #fff;
    margin-top: 40px;
    margin-left: 40px;
    margin-right: 20px;
    margin-bottom: 20px;
  }
```

一次指定四個方向的padding(順時鐘)
```css
  .blue-box {
    background-color: blue;
    color: #fff;
    padding: 40px 20px 20px 40px;
  }
```

一次指定margin
```css
margin: 40px 20px 20px 40px;
```

### Attribute Selector
當attribute`type`是checkbox時
```
  [type='checkbox']{
    margin-top: 10px;
    margin-bottom: 15px;
  }
```

### Relative Unit
`em`和`rem`是相對長度
相對於該element本身的size
```css
  .red-box {
    background-color: red;
    margin: 20px 40px 20px 40px;
    font-size: 1.2em;
	padding: 1.5em;
  }
```

### CSS 繼承性

```css
  body {
    background-color: black;
    color: white;
    font-family: monospace;
  }
  
```

而class可以蓋過`body`style
```css
   .pink-text{
    color: pink;
  }
```

而style中的後者class會蓋過前者
```html
<style>
  body {
    background-color: black;
    font-family: monospace;
    color: green;
  }
  .pink-text {
    color: pink;
  }

  .blue-text{
    color: blue;
  }
</style>
<h1 class="pink-text blue-text">Hello World!</h1>
```

而`id` selector更可以蓋過 上述的style
```css
  #orange-text{
    color: orange;
  }
```

inline style還可以再蓋掉其他的style
```html
<h1 id="orange-text" class="pink-text blue-text" style="color: white;">Hello World!</h1>
```

`!important`可以防止style覆蓋的情況發生
```css
  .pink-text {
    color: pink !important;
  }
```

### 變數
```css
	.penguin{
		--penguin-skin: gray;
		
		background: var(--penguin-skin);
	}
```
`var(變數, 備用變數)` (Variable fallback)
```css
    background: var(--pengiun-skin, black);
```

然而IE並不支援CSS Variable，我們可以用多重declaration的方式
```css
  .red-box {
    
    background: red;
    background: var(--red-color);
    height: 200px;
    width:200px;
  }
```

變數之於class繼承性
`:root`這裡是偽class selector，而root通常是`html`element
```
  :root {

    --penguin-belly: pink;
  }

  body {
    background: var(--penguin-belly, #c6faf1);
  }
```

當然也可以覆蓋
```css
  :root {
    --penguin-belly: pink;

  }

  body {
    background: var(--penguin-belly, #c6faf1);
  }
  .penguin {
    --penguin-belly: white;
  }
```

### 藉由Media Query改變數
當瀏覽頁面的寬度小於350px時，root的變數會被覆蓋
```css
  @media (max-width: 350px) {
    :root {
        --penguin-size: 200px;
        --penguin-skin: black;
    }
  }
```

### 文字對齊
* `text-align: center;`
* `text-align: right;`
* `text-align: left;`
* `text-align: justify;` 除了最後一行之外，其他行填滿左右

```css
  h4 {
    text-align: center;
  }
  p {
    text-align: justify;
  }
```

### 寬高
`width: 245px;`
`height: 25px;`
```
  .fullCard {

    border: 1px solid #ccc;
    border-radius: 5px;
    margin: 10px 5px;
    padding: 4px;
    width: 245px;
  }
  h4 {
    text-align: center;
    height: 25px;
  }
```

### 粗體 斜體 底線

粗體
```html
 <strong> </strong>
```
```css
	font-weight: bold;
```

底線
```html
<u></u>
```
```css
	text-decoration: underline;
```

斜體
```html
<em></em>
```
```css
	font-style: italic;
```

刪除線
```html
<s></s>
```
```css
	text-decoration: line-through;
```

一條水平分隔線
```html
<hr>
```

### RGBA中的透明度
```css
  h4 {
    text-align: center;
    padding: 10px;
    background-color: rgba(45, 45, 45, 0.1)
  }
```

### [加上框式陰影](https://www.freecodecamp.org/learn/responsive-web-design/applied-visual-design/add-a-box-shadow-to-a-card-like-element)
`box-shadow`的屬性：
* `offset-x`
* `offset-y`
* `blur-radius`
* `spread-radius`
* `color`

用逗號分隔開多個陰影
```css
  #thumbnail{
    box-shadow: 0 10px 20px rgba(0,0,0,0.19), 0 6px 6px rgba(0,0,0,0.23)
  }
```

### Element 的不透明度
`opacity`不透明度
```css
  .links {
    text-align: left;
    color: black;
    opacity: 0.7;
  }
```

### 調整大小寫
`text-transform`
* `lowercase`
* `uppercase`
* `capitalize` 單字首大寫
* `inherit` 繼承自父element
* `none`

```css
  h4 {
    text-align: center;
    background-color: rgba(45, 45, 45, 0.1);
    padding: 10px;
    font-size: 27px;
    text-transform: uppercase;
  }
```

### 字體粗度
`font-weight`
```css
  h1 {
    font-size: 68px;
    font-weight: 800;
  }
```

### 行距
`line-height`
```css
  p {
    font-size: 16px;
    line-height: 25px;
  }
```

### 滑鼠在超鏈接上的style
`hover`
```css
  a {
    color: #000;
  }

  a:hover{
    color: red;
  }
```

### 相對位置
CSS 相對位置 offset property
`left` `right` `top` `bottom`
```css
p{
	position: relative;
	bottom: 10px;
}
```
![](https://cdn-media-1.freecodecamp.org/imgr/eWWi3gZ.gif)

### 絕對位置
```css
p{
	position: absolute;
	bottom: 10px;
}
```

### 固定位置
fixed positon不會隨著頁面卷動而移動
```css
 #navbar {

  

 position: fixed;

 top: 0px;

 left: 0px;

  

 width: 100%;

 background-color: #767676;

 }
```