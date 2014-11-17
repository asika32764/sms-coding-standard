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
選擇器之後的左大括號與右大括號須分別獨立存在於新的一行，且應與左大括號處於相同的縮排。

```css
/* 正確 */
.example
{
    color: #fff;
}

/* 錯誤 - 右大括號的位置錯了，沒有正確縮排 */
.example {
    color: #fff;
    }
```

相關的選擇器在同一行，不相關的選擇器在新的一行：

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

Commenting
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
   ========================================================================== */
```

### 長篇幅文字註解
```css
/**
 * 長篇幅文字註解描述使用 Doxygen 風格的註解格式,  
 *
 * 長篇幅的文字是用來註解不能簡單被瞭解的片段：不同的狀態，排列組合，條件，使用方式等等。
 *
 * TODO: 這是一個註解區塊中 todo 的範例，描述之後需要被完成的項目。
 *   一行應小於 80 個字元，換行之後須以兩個空白作為縮排開頭
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

Naming Convention
-----------------
A good naming convention will help your and your team [[3]]
  
- what type of thing a class does;
- where a class can be used;
- what (else) a class might be related to.

### BEM Methodology
#### Introduction
BEM - meaning blocks, elements and modifiers - is a front-end naming methodologies introduced by Yandex [[2]]. The architecture 
allows you maintaining your project with more flexibility and mantainability in a schematic manner. 
The point of OOCSS is to tell other developers what piece of markup is doing by looking its name.
You can easily understand the relationship of a child element and its precedent block.  

#### Blocks
Block was a part of a page design or layout whose specific and unique meaning was defined either semantically or visually [[8]]. Block is a visual and functional component of the interface. It is reusable and should be independently existed.

For example, Menu Block, Logo Block, Search Block, Auth Block.

<img src="images/blocks-example.png" alt="Blocks example" style="width: 200px;"/>

##### Naming Rule
Naming of blocks is quite simple. As long as the block is self-explaining. Single dash (-) is allowed if needed. (This could be alter with camelCase naming [[10]], wait for further discussion) 

- ```.button```
- ```.text-field```
- ```.flyout```
- ```.heading```
- ```.menu```

Or with prefix, ```b-``` for block, ```c-``` or ```j-``` for js block and ```g-``` for global etc.. Prefix is optional.
- ```.b-button```
- ```.b-text-field```
- ```.b-flyout```
- ```.b-heading```
- ```.b-menu```

HTML Example:
```html
<ul class="menu">
  <li>
    <a href="#">foo</a>
  </li>
  <li>...</li>
</ul>  
```

#### Elements
Element is a component part of block. It only exists within block and can not be used on its own outside of the block.
 
For example, Menu block has menu items, heading block has logo element and slogan element.

<img src="images/elements-example.png" alt="Elements example" style="width: 200px;"/>

##### Naming Rule 
Element use double underline(__) as a prefix. For example ```.block__element``` represents a descendent of ```.block```.

- ```.button__icon```
- ```.text-field__label```
- ```.flyout__title```
- ```.heading__logo```
- ```.menu__item```

HTML Example:
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

#### Modifiers
 ```Modifier``` in BEM is similar to ```State``` in SMACSS. It is used to defined the state of element or block.
 Multiple modifiers can be used on the same block simultaneously. 
 For example, a button block may have multiple states such as enabled, disabled or hover. Skin and theme could also be a modifier: shadowed, bordered etc..
 
 <img src="images/modifiers-example.png" alt="Modifiers example" style="width: 200px;"/>

##### Naming Rule
For modifier, we use double hyphens(--) as prefix which was first introduced in this article [MindBEMding][6]. 
If the name name of that modifier is too long, also separate it with double hyphens. (This could be alter, wait for further discussion.)

- ```.button--theme-green```
- ```.text-field--disabled```
- ```.flyout--align--top```
- ```.heading--dark--background```
- ```.menu__item--promo```

HTML Example:
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

#### Quick Summarize
- ```.block {…}```
- ```.block—-modifier {…}``` 
- ```.block__element {…}```
- ```.block__element—modifier {…}```

#### More Sophisticated Examples

##### Drop tag names and IDs
By following BEM (or any other methodology), we no longer need to use tag names and IDs as selectors. In fact, 
we should never use tag names and IDs, this may result in faster selectors and faster render time.

##### Reuse same semantics block on any tag
```html
<div class="block"></div>
<span class="block"></span>
<table class="block"></table>
```

##### CSS Specificity problem solved
CSS selector has priority rules, that is, by specifity first, then by rule order. Oftenly, 
overwriting other developers' selector will result like this due to specificity:
 
```css
#jsn_form_5 .form-actions .form-extra-message {
  font-size: 1.4em;
  color: #c25b5b;
  margin: 6px 0;
}
#jsn_form_7 .form-actions .form-extra-message {
  font-size: 1.4em;
  color: #c25b5b;
  margin: 6px 0;
}
```

Thanks to the OOCSS methodologies, blocks are independent and decouple with html tags.  

##### LESS
We may write our less code in nested way:
```sass
.block {
    &__element {
        &--modifier {
        }
    }
}
```
This will output:
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

#### Downside
##### Ugly?!
I know.

But after all, it's all about consistency, readability, and maintainability.

Whilst the CSS language doesn't actually allow object-oriented programming, following a syntax structure like BEM can still enforce the consistency between projects.
Without consistency, taking-off the projects other people hand to you may cause you spending more time on trying to figure out what their code really does.

For example, one might be curious what's the difference between '2-3 classes chained together' versus '2-3 parts separated by dashes and underscores(uhhh)'? 

```html
<a class='btn btn-large'>
```

The former one implied that there might be 2-3 different classes, and this will be confusing to future maintainers because
they won't understand why there are 3 classes on an element and the relationship among classes is unclear.
In our example is whether ```btn-large``` is sufficient on its own, or whether it depends on the class btn being present? Is the base style defined in ```.btn``` only or both in ```.btn, .btn-large```?
Then what if someone forget to include ```.btn```?

##### Fragmentation
Since the merit of BEM is to isolate every visual block. Your CSS might end up with tons of modifier classes when you find yourself with 10 different link styles, 12 shades of blue, 18 subtly different button styles[11] etc..
 
#### Future Methodology
Don't like '__-__---_-__-'?

There is a promising elegant solution called <b>AM - Attribute Modules for CSS</b>[[11]] [[12]], I highly recommend you read through it.

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
然而隨著 Pre-processor 的流行以及 OOCSS 的命名規則出現，其實避免相同的樣式片段重複出現的問題。

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