SMS-CSS-Guidelines
==================
A CSS draft guidelines to discuss. 
We will try to adopt object-oriented CSS methodology in this draft.

High-Level Principle
--------------------
### Good CSS Architecture [1]
- Predictable 
- Reusable 
- Maintainable 
- Scalable

Syntax and Formatting
---------------------

Commenting
----------

Naming Convention
-----------------
A good naming convention will help your and your team [3]
  
- what type of thing a class does;
- where a class can be used;
- what (else) a class might be related to.

### BEM Methodology
#### Introduction
BEM - meaning blocks, elements and modifiers - is a front-end naming methodologies introduced by Yandex [2]. The architecture 
allows you maintaining your project with more flexibility and mantainability in a schematic manner. 
The point of OOCSS is to tell other developers what piece of markup is doing by looking its name.
You can easily understand the relationship of a child element and its precedent block.  

#### Blocks
Block was a part of a page design or layout whose specific and unique meaning was defined either semantically or visually [8]. Block is a visual and functional component of the interface. It is reusable and should be independently existed.

For example, Menu Block, Logo Block, Search Block, Auth Block.

<img src="images/blocks-example.png" alt="Blocks example" style="width: 200px;"/>

##### Naming Rule
Naming of blocks is quite simple. As long as the block is self-explaining. Single dash (-) is allowed if needed. 

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
  <li class="menu__item--promo">
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
 
#### Ugly?!
 
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

[1]: http://philipwalton.com/articles/css-architecture/ 
[2]: http://bem.info/ "by Yandex"
[3]: http://cssguidelin.es/
[4]: http://www.slideshare.net/kurotanshi/css-oocss-smacss-bem
[5]: https://github.com/bjankord/CSS-Components-Modifiers-And-Subcomponents-Collection
[6]: http://csswizardry.com/2013/01/mindbemding-getting-your-head-round-bem-syntax/
[7]: http://www.slideshare.net/VarvaraStepanova/bem-it-introduction-to-bem-methodology
[8]: http://www.smashingmagazine.com/2013/02/21/the-history-of-the-bem-methodology/
