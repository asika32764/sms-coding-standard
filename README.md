# SMS 軟體工程編碼標準文件 v0.1.0

## 前言

編碼標準是軟體工程中的重要組成部分，用以規範工程師的寫作、排版與命名，並保持一致性，使程式碼可讀性提高，讓軟體易於維護。

本標準文件為 SMS 工程師參考用編碼標準，基於 Joomla! 編碼標準，簡化部分非 Open source 所需之繁雜規定，並以範例形式展示。

### Joomla! 編碼標準

請參照 [Joomla-Coding-Stanard-Chinese](https://github.com/asika32764/Joomla-Coding-Stanard-Chinese)


## 檔案格式

### 編碼

請一律使用未帶 BOM 的 UTF-8 編碼格式。

### 換行

編輯器請設定成以 `LF` (`\n`) 作為換行字元。請勿使用 Mac 的回車符 `CR` (`\r`) 或 Windows 的 `CRLF` (`\r\n`) 組合。

Windows 安裝 Git 時，請選擇 `Checkout Windows-style, commit Unix-style line endings` 選項。

![git-crlf](http://cl.ly/T2xQ/git-crlf.png)

參見： ![Git 在 Windows 平台處理斷行字元 (CRLF) 的注意事項](http://blog.miniasp.com/post/2013/09/15/Git-for-Windows-Line-Ending-Conversion-Notes.aspx)


## 基礎編輯設定

### PHP 標籤

永遠使用長標籤： `<?php ?>` 來包裹 PHP 程式碼，不使用短標籤 `<? ?>`。這可以確保您的程式碼可執行在大多數未經設定的主機環境。

如果檔案中只包含PHP程式碼，則不應該包含結尾標籤 `?>`。這個標籤在 PHP 中不是必要的。這樣子可以避免在系統輸出前，不小心讓任何空白預先送出 header ，這會造成 Joomla 的 Session 功能錯誤 (參見 PHP 手冊的說明 [Instruction separation](http://php.net/basic-syntax.instruction-separation))。

永遠保留一行空行在檔案結尾，範例：

``` php
<?php

class Foo
{

}

```

### 縮排與對齊

程式縮進請使用 Tab 而非空白字元，註解與變數指派的排版對齊應使用空白字元。

範例：

``` php
/**
 * The foo function.
 *
 * @return void
 */
function foo()
{
	$a    = 'a';
	$bar  = 'bar';
	$cool = 'cool';
}
```

### 行寬

原則上每行程式碼並沒有最大長度限制，但根據國際標準值，150字元能夠在不需要水平滾動的狀況下達到最好的可讀性。
若遇到換行會影響輸出結果的情況(例如 PHP/HTML 混合的結構檔案)，更長的程式碼也是被允許的。


## 程式寫作規範

### 引入程式

當手動直接載入程式檔案時，請用 `require` 與 `require_once`，若採用程式動態載入（例如使用 `Factory` 模式），則使用 `include` 與 `include_once`。

引入程式請以關鍵字寫法，不要用函式寫法。

正確：

``` php
require_once 'foo.php';
```

不應使用括號：

``` php
require_once('foo.php');
```

一般來說，我們應該盡量用絕對路徑，搭配 Joomla! 常數來引入檔案，避免位置變更時出錯：

``` php 
require_once JPATH_LIBRARIES . '/foo/bar.php';
```

若要採用相對路徑，也應該使用 `__DIR__` 來當做路徑基礎：

``` php
require_once __DIR__ . '/../bar.php';
```

## 程式排版

### 控制結構

所有的控制結構必須在關鍵字與起始括號之間放置一個空白字元，而開頭、結尾括號與邏輯判斷式之間無空格。這是為了區隔控制結構與函式以方便辨認，而括號內必須要包含邏輯。

控制結構關鍵字，如： `if`, `else`, `do`, `for`, `foreach`, `try`, `catch`, `switch` 與 `while` 皆採 [Allman](http://en.wikipedia.org/wiki/Indent_style#Allman_style) 風格，關鍵字本身必須在一個新行，而語言區塊（大括號）的開頭與結束也接需再一個新行中。

### _if-else_ 範例

```php
if ($test)
{
	echo 'True';
}
// 註解可寫在此
// 要注意的是 "elseif" 採用單一單字而非拆開成 "else if"
elseif ($test === false)
{
	echo 'Really false';
}
else
{
	echo 'A white lie';
}
```

如果控制結構的判斷式需要多行，則第二行開始需要一個 Tab 縮排，結尾括號需要再同一行上。

```php
if ($test1
	&& $test2)
{
	echo 'True';
}
```

### _do-while_ 範例


```php
do
{
	$i++;
}
while ($i < 10);
```

### _for_ 範例

```php
for ($i = 0; $i < $n; $i++)
{
	echo 'Increment = ' . $i;
}
```

### _foreach_ 範例

```php
foreach ($rows as $index => $row)
{
	echo 'Index = ' . $id . ', Value = ' . $row;
}
```

### _while_ 範例

```php
while (!$done)
{
	$done = true;
}
```

### _switch_ 範例

當使用 `switch` 時， `case` 關鍵字必須縮排一次，而 `break` 關鍵字必須獨立在新的一行，且相較於 `case` 再縮排一次。

```php
switch ($value)
{
	case 'a':
		echo 'A';
		break;

	default:
		echo 'I give up';
		break;
}
```

#### 關於 Allman 風格

採用 Allman 風格的優點在於，我們可以隨時註解或替換控制結構，而不會造成語言錯誤。例如：

``` php
// if ($egg)
{
	echo 'coffee';
}
```

``` php
// for ($i = 0; $i <= count($array); $i++)
foreach ($array as $i => $value)
{
	// Do something...
}
```

以上寫法皆可以正常運作。

除此之外，我們不必為了程式碼可讀性刻意在控制結構前後增加空行：

``` php
if ($yoo)
{
	echo '123';
}
else
{
	echo '321';
}
```

比起：

``` php
if ($yoo) {
	echo '123';
} else {
	echo '321';
}
```

有較佳可讀性，雖然可能造成程式碼文件較長。

## 類別與其成員宣告

### 類別

類別採用駝峰式 (CamelCase) 命名法，開頭大寫，例如： `ContentModelArticle` 或 `FGHElper`

前後括號各自為一個新行，括號與內容之間不應該有空行。除了 Alias 以外每個檔案應該只有一個類別，`extends` 與 `implement` 應該與類別名稱在同一行。

### 函式與方法

採用 "studly caps" 風格 (也稱作 "bumpy case" 或 "camel caps")，起始字母小寫，每個單字開頭大寫，範例： `getItems()`。

前後括號各自為一個新行，方法與方法之間（包含其註解區塊）應該只有一行空行。

方法宣告應搭配權限關鍵字，非公開介面應該盡量以 `protected` 為主，讓子代類別可以取用父代方法，公開介面則應該搭配 `public`。

### 類別屬性

Joomla! CMS 中，類別屬性以底線分隔單字，如： `$this->default_view`，以跟方法坐區隔。但在 Framework 中，屬性也改以"studly caps" 風格。因此僅規範專案統一即可。

屬性宣告應搭配權限關鍵字，如 `public`、`protected`、`private`。若非特別必要，預宣告屬性應該以 `protected` 為主，讓子代類別可以存取父代屬性，而外部則依靠 getter 與 setter 來存取。

若屬性沒有初始值，則一定為 `null`，沒有特殊目的則不需強制指派初始值。

### 常數

常數應永遠為大寫，並用底線分隔單字，根據專案加上前綴字。例： `BAMAHOME_ADMIN`。

### 宣告範例

``` php
<?php

class ContentModelArticle extends JModelLegacy
{
	public $foo;
	
	public function getFoo()
	{
		return $this->foo;
	}
}
```

## 一般變數宣告及使用

### 賦值

一般變數建議集中於方法開頭進行宣告或賦值，可依據變數長度適度排版，等號距離最長變數應該只有一個空格：

``` php
public function getItems($pk = null)
{
	$pk    = (int) $pk ?: $this->input->getInt('id');
	$db    = JFactory::getDbo();
	$app   = JFactory::getApplication();
	$query = $db->getQuery(true);
	
	// 函式主體
}
```

### 設定值或運算常數

某些演算法，或固定數值的參數，我們不應該直接將數值寫死在運算中，例如：

``` php
foreach ($array as $k => $value)
{
	if ($k == 3)
	{
		break;
	}
	
	// Do some stuff....
}
```

這會讓使用者混淆，不知道 `3` 這個數字是怎麼來的，當多組數字共存時，會造成日後修改參數的麻煩。我們應該預先宣告這些數字，並給予語意化的名稱：

``` php
$limit = 3;

foreach ($array as $k => $value)
{
	if ($k == $limit)
	{
		break;
	}
	
	// Do some stuff....
}
```

或是建立設定擋來方便修改：

``` php
class ImageThumb
{
	protected $width;
	
	protected $height;
	
	public function __construct(JRegistry $config)
	{
		$this->width  = $config->get('thumb.width', 640);
		$this->height = $config->get('thumb.height', 480);
	}
}
```

## 陣列

陣列元素的指派可稍微排版，當多行時，可用 Tab 縮排。每行跟隨一個都逗號結尾，最後一行可包含逗號，這是 PHP 允許的寫法，對於程式碼 diff 比對時也有所幫助。

範例:

```php
$options = array(
	'foo'	=> 'foo',
	'spam'	=> 'spam',
);
```

若確保環境為 PHP 5.4 ，可使用短宣告語法：

``` php
$array = ['a', 'b', ['c', 'd']];
```

## 函式與方法呼叫

### 一般函式與方法調用

直接於函式或方法後驗接上括號，不需要空格，以此與控直結構區隔：

``` php
$item = $foo->getItem($pk);
```

### 鏈狀調用

若物件支援鏈狀調用，除了第一次調用以外，需要換行並縮排一次，無需對齊物件變數，且結尾直接跟著分號：

``` php
$query->select('u.*')
	->from($db->qn('#__users') . ' AS u'))
	->where($db->qn('id') . ' = ' . $db->q($pk));
```

調用後行寬較短時可考慮不換行：

``` php
$db->setQuery($query)->loadResult();
```

## 判斷式

### 運算子

使用 `&&` 與 `||` 運算子而非 `and` 與 `or` 運算子。

### 大小於判斷

根據語意化決定使用 `> 0` 還是 `>= 1` ，以易懂為主。

### 三元運算

運算子前後應空格，分號前不空格。若過長的三元運算子，可考慮換行處理，但運算子必須在開頭，換行後縮進一次。

範例：

``` php
echo $alias ? 'Alias' : 'Title';
```

``` php
echo ($config->get('item.alias') == $alias)
	? $this->item->get('alias')
	: $this->item->get('title', $default);
```

確保為 PHP 5.3 的環境可用簡寫：

``` php
$foo = $bar ?: $yoo;
```

### 存在判斷

當我們為了避免因變數或陣列元素未宣告而造成 Notice 時，可考慮用專用的判斷函式在 if 中。

`isset()` 用在判斷變數或陣列是否宣告過，且值不為 null：

``` php
if (isset($array['eggs']) && $array['eggs'] == 5)
{
}
```

`empty()` 用在判斷變數或陣列元素是否被宣告過且值不為否（含 `null`, `false`, `0`, `''`, `array()`）等，一般作為布林值判斷，且內容是動態的，可能不曾被初始化時才用：

``` php
if (!empty($array['online']))
{
}
```

注意 `isset()` 在變數為 `null` 時會回傳否，因此判斷物件屬性是否被宣告過，應該用 `property_exists()`。

若我們能夠確保變數或物件元素一定存在，請大膽直接將他放在判斷式中，此為慣例寫法，表達性佳不會有混淆問題：

``` php
if ($yoo)
{
	echo 'GO';
}
elseif (!$hoo)
{
	echo 'Back';
}
```

避免多重否定寫法混淆使用者：

``` php
if (!is_null((bool) $qoo))
{
}
```


