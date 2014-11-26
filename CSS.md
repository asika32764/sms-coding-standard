SMS-CSS-Guidelines
==================
A CSS draft guidelines to discuss.
在這份 CSS 指引中我們會嘗試採用物件導向 CSS 設計(OOCSS)，並大量使用 Joomla Coding Standard 中所提供的 CSS 指引。


High-Level Principle
--------------------
### Good CSS Architecture [[1]]
- 可預測 Predictable 
- 可重複使用 Reusable 
- 考維護性 Maintainable 
- 可擴充 Scalable

Syntax and Formatting
-------------------------
### 樣式屬性格式
每一個屬性都應該存在獨立的一行，並縮排一個層級。冒號之前不應該有空白字元，但須後綴一空白字元。所有的樣式屬性須以分號 (;) 作為結尾。
```css
/* 正確 */
.example {
    background: black;
    color: #fff;
}

/* 錯誤 - 冒號後面沒有後綴空白 */
.example {
    background:black;
    color:#fff;
}

/* 錯誤 - 沒有以分號作為結尾 */
.example {
    background: black;
    color: #fff
}
```

### 縮排
以4個空白(spaces)作為縮排。

```css
/* 正確 */
.example {
	color: #000;
	visibility: hidden;
}

/* 錯誤 - 寫在同一行 */
.example {color: #000; visibility: hidden;}
```

### 巢狀結構
LESS/SCSS 等等的 Pre-compiled CSS 允許巢狀結構，在巢狀結構中，其子選擇器還有樣式規則都應該縮排(4spaces)。巢狀結構的頭尾都應以一行空行作為間隔。
```css
/* 正確 */
.example {

  > li {
    float: none;

	+ li {
		margin-top: 2px;
		margin-left: 0;
	}

  }

}
```

### 對齊

#### 選擇器及宣告
左大括號必須跟選擇器位於同一行，並前綴一空白字元。右大括號須存在於最後一個屬性規則之後並獨立於新的一行，且應與左大括號處於相同的縮排。

```css
/* 正確 */
.example {
    color: #fff;
}

/* 錯誤 - 右大括號的位置錯了，沒有正確縮排 */
.example 
{
    color: #fff;
    }
```

各個選擇器皆獨立在自己的一行，最後一個選擇器與左大括號位於同一行：

```css
.foo, .foo--bar,
.baz {
    display: block;
}
```

#### 樣式宣告對齊
同類型或類似的樣式宣告，建議使用空白來縮排對齊，這對可以例如：

```css
.foo {
    -webkit-border-radius: 3px;
       -moz-border-radius: 3px;
            border-radius: 3px;
}

.bar {
    position: absolute;
    top:    0;
    right:  0;
    bottom: 0;
    left:   0;
    margin-right: -10px;
    margin-left:  -10px;
    padding-right: 10px;
    padding-left:  10px;
}
```

### HEX 值
HEX 值應該使用小寫並以最小縮寫宣告：

```css
/* 正確 */
.example {
    color: #eee;
}

/* 錯誤 */
.example {
    color: #EEEEEE;
}
```

### HTML 屬性選擇器
屬性選擇器須以雙引號包含。

```css
/* 正確 */
input[type="button"] {
    ...
}

/* 錯誤 - 沒有雙引號 */
input[type=button] {
    ...
}

/* 錯誤 - 使用單引號 */
input[type='button'] {
    ...
}
```

### 零值的單位
零值不應該使用單位。

```css
/* 正確 */
.example {
   padding: 0;
}

/* 錯誤 - 使用單位 */
.example {
   padding: 0px;
}
```

註解
----------
在 SMS 中，專案數量龐大，詳細的註解有助於在不同的專案間快速切換與理解。加上因為 CSS 語言特性的關係，CSS 有許多情況是無法立即被瞭解的，舉例來說：

- 當你的這段 CSS 程式碼相依於其他 CSS 的時候;
- 當你改變這段 CSS 會在何處照成影響;
- 這段 CSS 還被使用在什麼地方;
- 作者希望這段 CSS 

總結來說，你必須對那些無法從該程式碼片段中一眼就了解的事。舉例來說，你不需要針對 ```color: red;``` 作註解。

### 主要段落
主要的程式碼段落必須以完整的註解區塊作為開頭，例如：

```css
/* ==========================================================================
   PRIMARY NAVIGATION
   ========================================================================== */
```

### 次要段落
次要段落須以開放式的註解區塊為開頭：

```css
/* Mobile navigation
   -------------------------------------------------------------------------- */
```

### 長篇幅文字註解
```css
/**
 * 長篇幅的文字是用來註解不能簡單被瞭解的程式碼片段：如不同的狀態，排列組合，使用條件，使用方式，使用時機等等。
 * 
 * @tag This is a tag named 'tag'
 * 
 * TODO : 這是一個註解區塊中 todo 的範例，描述之後需要被完成的項目。
 *   一行應小於 80 個字元，換行之後須以兩個空白作為縮排開頭
 */
``` 

如 [CSS Wizardry](http://csswizardry.com/) 裡的範例：
```css 
/**
 * The site's main page-head can have two different states:
 *
 * 1) Regular page-head with no backgrounds or extra treatments; it just
 *    contains the logo and nav.
 * 2) A masthead that has a fluid-height (becoming fixed after a certain point)
 *    which has a large background image, and some supporting text.
 *
 * The regular page-head is incredibly simple, but the masthead version has some
 * slightly intermingled dependency with the wrapper that lives inside it.
 */
 ```

### Extend Style
在 OOCSS 中不同的 CSS 元件可能被放在不同的檔案裡，你可能會遇到此某兩個 component 有互相關聯的情形。如，某一個 button 的 bass class 在另一
個檔案中被新的 button 所擴充加上新的 style，須在兩邊檔案都寫上註解。如下：

在 Base Object 的檔案中：
```css
/**
 * Extend `.btn {}` in _components.buttons.scss.
 */

.btn {}
```

在 擴充的主題檔案中：
```css
/**
 * These rules extend `.btn {}` in _objects.buttons.scss.
 */

.btn--positive {}

.btn--negative {}
```

命名規則
-----------------
好的命名規則，可以幫助你和你的團隊快速瞭解 [[3]]：

- 這個 class 在做什麼事
- 可以在什麼情境使用此 class
- 這個 class 可能跟什麼有關聯 

### BEM 方法論
#### 簡介
BEM - blocks, elements 和 modifiers 的縮寫 - 是前端命名的方法論之一，由 Yandex 所提出 [[2]]。
BEM 的語意化(schematic)的命名和物件導向架構，讓程式碼在維護上擁有更多的擴充彈性與可讀性。
OOCSS 的精神，是讓不同的開發者可以透過觀察 markup 的命名方式快速地了解到某一段程式碼的功用。
開發者也可以不費力的看出子元件跟其父原件之間的關聯性。

#### 區塊 (Blocks)
區塊 (Blocks) 是網頁面設計上的一個區塊，該區塊在視覺上，功能上或是語意結構上有其特別的意義 [[8]]。Blocks 可以重複使用，並且獨立存在不和其他元件有關聯。 
例如：Menu Block, Logo Block, Search Block, Auth Block.

<img src="images/blocks-example.png" alt="Blocks example" style="width: 200px;"/>

##### 命名規則
Block 的命名方式很簡單。只要其命名是具有意義且可以自我說明 (self-explaining) 的即可。必要的話可以以破折號 (dash) 隔開，也有使用駝峰式命名的做法 [[10]]，待討論。

- ```.button```
- ```.text-field```
- ```.flyout```
- ```.heading```
- ```.menu```

或是可以自定義前綴字元, ```b-``` 代表 block，```c-```、```js-``` 或 ```j-``` 代表 js block 以及 ```g-``` 代表 global 等等。前綴字元的使用是選擇性的.
- ```.b-button```
- ```.b-text-field```
- ```.b-flyout```
- ```.b-heading```
- ```.b-menu```

HTML 範例:
```html
<ul class="menu">
  <li>
    <a href="#">foo</a>
  </li>
  <li>...</li>
</ul>  
```

#### 元素 (Elements)
元素 (Elements) 是隸屬於區塊下的元素組成，元素只能存在於區塊之內，不能在其所屬之區塊結構外面所使用。
例如：Menu block 有 menut items, heading block 則有 logo 元素和 slogan 元素。
 
<img src="images/elements-example.png" alt="Elements example" style="width: 200px;"/>

##### 命名規則
元素的命名規則為在前綴兩個底線 (__)，雙底線之前是區塊命名。例如 ```.block__element``` 代表 element 是屬於 ```.block``` 的子元素。

- ```.button__icon```
- ```.text-field__label```
- ```.flyout__title```
- ```.heading__logo```
- ```.menu__item```

HTML 範例:
```html
<ul class="menu">
  <li class="menu__item">
    <a href="#">foo</a>
  </li>
  <li class="menu__item">
    <a href="#">bar</a>
  </li>
</ul>  
```

#### 修改器 (Modifiers)
BEM 的修改器 (Modifier) 類似 SMACSS 的"狀態"。修改器是拿來定義元素或區塊的狀態。一個區塊可以同時擁有不同的修改器。
例如，一個按鈕可以有不同的狀態，分別是 "enabled"、"disabled" 或 "hover"。除了狀態之外，區塊的皮膚 (skin) 或主題 (theme) 也可以是修改器的一種：陰影、邊框等等。

<img src="images/modifiers-example.png" alt="Modifiers example" style="width: 200px;"/>

##### 命名規則
修改器的命名我們使用兩個破折號 (--) 作為前綴字元 ([MindBEMding][6])。
如果修改器的名字太長，必要時可以使用一個破折號隔開。

- ```.button--theme-green```
- ```.text-field--disabled```
- ```.flyout--align--top```
- ```.heading--dark--background```
- ```.menu__item--promo```

HTML 範例:
```html
<ul class="menu">
  <li class="menu__item menu__item--promo">
    <a href="#">foo</a>
  </li>
  <li class="menu__item">
    <a href="#">bar</a>
  </li>
</ul>  
```

#### 小結
- ```.block {…}```
- ```.block—-modifier {…}``` 
- ```.block__element {…}```
- ```.block__element—modifier {…}```

#### 延伸 Tips

##### 避免使用 HTML tag 名稱以及 IDs 作為選擇器
我們應該盡量避免使用 HTML tag 名稱作為選擇器，並完全避免使用 IDs 作為選擇器。避免使用 HTML tag 的原因是希望讓 CSS 跟 HTML 解耦合，讓其不依賴 HTML 結構以增加可讀性以及維護性。
不使用 IDs 作為選擇器是因為一個 ID 是獨立且唯一存在於 HTML Markup 中，如果用了 ID 當選擇器，代表該 CSS 程式碼片段不能被重複使用。

##### 可以重複使用同樣區塊在任意的 tag 上 
```html
<div class="block"></div>
<span class="block"></span>
<table class="block"></table>
```

##### 解決了 CSS 選擇器的優先性 (specificity) 問題
BEM 建議將 Modifiers 使用如下 ```<div class="block block__mod">``` [[16]]，並獨立為 ```.block__mod``` 寫 style。

舉例來說：
```html
<div class="header">
  <button class="button active">
</div>
```
如果你用的是組合的選擇器 (Combined Selectors) 寫法 ```.button.active``` 會跟透過結合其父結構 ```.header .button```來覆寫 style 時擁有一樣的優先性，造成複寫的困難。
將 modifiers 分開地應可以避面這樣的問題。

##### LESS
透過 Pre-processor 語言的特性，我們可以使用巢狀結構來寫：
```sass
.block {
    &__element {
        &--modifier {
        }
    }
}
```
這會產生:
```css
.block {}
.block__element {}
.block__element--modifier {}
```

##### Real-World Frameworks Implemented in BEM style
Adobe Topcoat

http://topcoat.io/

inuit.css - Powerful, scalable, Sass-based, BEM, OOCSS framework.

https://github.com/csswizardry/inuit.css

#### 壞處
##### 長很醜?!
是的，我懂.

但 OOCSS 其背後目的, 是為了讓各個不同的開發者在開發程式時都能維持一致性，可讀性，以及可維護性。

因為 CSS 語言及架構特性並不是真正的物件導向語言，使用像 BEM 此類的方法論，可以加強不同專案間的一致性。
如果沒有一致性，接手別人的專案會讓你花上許多時間在看懂對方的程式片段真正的目的。

例如：
```html
<a class='foo bar baz'>
```
如果我們有 2-3 種不同的 classes，這會對未來的維護者造成混肴，因為 class 之間的關係並不明顯。

```html
<a class='btn btn-large'>
```
在這個範例中 ```btn-large``` 是否能獨立使用，或著需要相依於 ```btn``` 類別？Base style 只被定義在 ```.btn``` 或者是每個類別都共有 ```.btn, .btn-large```？如果有開發人員忘了加上```.btn```會發生什麼事？

#### Future Methodology
覺得 '__-__---_-__-' 很醜?

有一些新的方法論利用 css ```比較選擇器``` 的特性來操作 ```data-*``` 屬性，稱作 <b>AM - Attribute Modules for CSS</b>[[11]] [[12]]，推薦閱讀。

元件的 Modifiers[[14]]
---------------
一個 Base 元件通常有各種不同具有些微差異的 Styles，例如：Bootstrap 的 ```.btn``` 有 ```.btn-large``` 和 ```.btn-small``` 等等的變化。
有兩個主流的做法，分別是 "single-class" 和 "multi-class" 的 pattern。兩種 Class 各有優缺點。

### "single-class" 模式
```css
.btn, .btn-primary { /* button base styles */ }
.btn-primary { /* styles specific to primary button */ }
```
```html
<button class="btn">Default</button>
<button class="btn-primary">Login</button>
```
在 "single-class" 中，同樣的 style 被定義在多個 classes 上，好處是 html 的元素只需使用單一的 class。

### "multi-class" 模式
```css
.btn { /* button base styles */ }
.btn-primary { /* styles specific to primary button */ }
```
```html
<button class="btn">Default</button>
<button class="btn btn-primary">Login</button>
```

"multi-class"，是以模組化的方式將 base style 和 modifiers 分別定義在不同 classes 上，一個元件需要同時使用多個 classes。是比較適合擴充的模式。

### 延伸
一般使用上我們推薦 "multi-class" 的模式(如：Bootstrap)，原因是因為可將 css 程式碼物件導向化使其易於維護並且避免 "single-class" 中程式碼片段重複的問題。
然而隨著 Pre-processor 的流行以及 OOCSS 的命名規則出現，其實可以避免相同的樣式片段重複出現的問題。

由於 SMS Taiwan 使用 LESS，建議使用 ```extend()``` 的做法。

#### Pre-Processor 以 LESS 為例
透過 ```extend()``` 的 mixin，讓所有的子 Component/Element 都能繼承 base class。
```css
.btn{
  border: 2px solid #fff;
  …
}

.btn--large{
  &: extend(.btn all)
  font-size: 20px;
  …
}
```

### css 選擇運算子 ```^=```
選擇運算子 ```^=``` 可以選擇以等號後字串為開頭的參數，如：

```
// Base Class (以 btn 為開頭的 class, ex: btn--blue, btn--large) 
[class^="btn"] {
  border: 1px solid #666;
  padding: .3rem .6rem;
  display: inline-block;
}

// Modifiers
.btn--blue {
  background-color: lightblue;
  color: #fff;
  border: 1px solid #cbcbcb;
}
```
 
Credits
-------
1. [CSS Architecture](http://philipwalton.com/articles/css-architecture/) by Philip Walton
2. [BEM](http://bem.info/) by Yandex
3. http://cssguidelin.es/
4. http://www.slideshare.net/kurotanshi/css-oocss-smacss-bem
5. https://github.com/bjankord/CSS-Components-Modifiers-And-Subcomponents-Collection
6. http://csswizardry.com/2013/01/mindbemding-getting-your-head-round-bem-syntax/
7. http://www.slideshare.net/VarvaraStepanova/bem-it-introduction-to-bem-methodology
8. http://www.smashingmagazine.com/2013/02/21/the-history-of-the-bem-methodology/
9. http://www.sitepoint.com/css-sass-styleguide/
10. https://github.com/suitcss/suit/blob/master/doc/naming-conventions.md#components
11. http://glenmaddern.com/articles/introducing-am-css
12. http://amcss.github.io/
13. http://topcoat.io/
14. http://nicolasgallagher.com/about-html-semantics-front-end-architecture/
15. http://benfrain.com/multiple-classes-ui-component-variations-wrong/
16. http://getbem.com/faq/

[1]:  http://philipwalton.com/articles/css-architecture/ 
[2]:  http://bem.info/ "by Yandex"
[3]:  http://cssguidelin.es/
[4]:  http://www.slideshare.net/kurotanshi/css-oocss-smacss-bem
[5]:  https://github.com/bjankord/CSS-Components-Modifiers-And-Subcomponents-Collection
[6]:  http://csswizardry.com/2013/01/mindbemding-getting-your-head-round-bem-syntax/
[7]:  http://www.slideshare.net/VarvaraStepanova/bem-it-introduction-to-bem-methodology
[8]:  http://www.smashingmagazine.com/2013/02/21/the-history-of-the-bem-methodology/
[9]:  http://www.sitepoint.com/css-sass-styleguide/
[10]: https://github.com/suitcss/suit/blob/master/doc/naming-conventions.md#components
[11]: http://glenmaddern.com/articles/introducing-am-css
[12]: http://amcss.github.io/
[13]: http://topcoat.io/
[14]: http://nicolasgallagher.com/about-html-semantics-front-end-architecture/
[15]: http://benfrain.com/multiple-classes-ui-component-variations-wrong/
[16]: http://getbem.com/faq/