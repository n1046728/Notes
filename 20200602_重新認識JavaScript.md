# 重新認識 JavaScript筆記
## Content  
>[Day 02 JavaScript 簡介](#day-02-javascript簡介)  
>[Day 03 變數與資料型別](#day-03-變數與資料型別)  
>[Day 04 物件、陣列及型別判斷](#day-04-物件陣列及型別判斷)  
>[Day_05_JavaScript_是「傳值」或「傳址」？](#day-05-javascript-是傳值或傳址)  
>[Day 06 運算式與運算子](##Day&nbsp;06&nbsp;運算式與運算子)  
## Day 02 JavaScript簡介
### JavaScript誕生與目標
>早期網路速度28.8kbits/s的速率，網頁表單驗證透過後端驗證，不具效率，NetScape開發在瀏覽器執行的語言，處理該類簡單的驗證。

### ECMAScript與JavaScript的關係
>ECMAScript 是 Javascript 的標準，，ECMA-262 標準是規格書，而 JavaScript、JScript 這類語言，是實作的產品。

### ECMAScript History
* 1997 ES1
* 1998 ES2
* 1999 ES3
* 2009 ES5
* 2015 ES2015(ES6)
* 2016 ES2016
* 2017 ES2017
---

## Day 03 變數與資料型別
### 變數
* ES6以前宣告變數可透過**var**，ES6以後宣告變數與常數還可以使用**let**與**const**來宣告
* 弱型別：變數本身無須宣告型別，型別的資訊只在值或物件本身，變數只用來作為取值或物件的參考
* 未透過var宣告的變數為全域變數

### 資料型別
* 變數沒有型別，值才有
* string number boolean null undefined，ES6後多了Symbol
* 可用typeof判斷型別

#### string
* javascript 沒有char字元的概念，只有字串可用單引號或雙引號包覆
* escape character **\\**
* 多行字串換行 <strong>/</strong>

#### number
* javascript只有一種數值型別，小數非小數都是此類
* 實作IEEE 754，要取得精確數則使用[number-precision](https://github.com/nefe/number-precision)
* 特殊數字 Infinity(正無窮) -Infinity(負無窮) NaN(Not a Number)
  * NaN與任何數值運都為NaN
  * NaN不等於自己
  * isNaN(value)判斷是否為NaN 

```javascript
typeof(NaN) //number
NaN === NaN //false
isNaN(NaN) //true
```
#### boolean
* 所有東西都可以隱含轉換為boolean

#### null & undefined
* undefined：代表(此變數)還沒給值，所以不知道是什麼
* null：代表(此變數可能曾經有值，或可能沒有值)現在沒有值
* 非全域範圍下undefined可以做為變數名稱
```javascript
Number(null) //0
Number(undefined) //NaN
```
---
## Day 04 物件、陣列及型別判斷
### 物件Object
* 所有基本型別(Primitives)外的值都是物件
* 一個物件可以是零至多種屬性的集合，而屬性是鍵(key)與值(value)之間的關聯
#### 建立物件
* 早期建立的方式
```javascript
var person = new Object();
person.name = 'james';
person.job = "backend developer";
person.sayName = function(){
    alert(this.name)
};
```
* 物件實字(Object literal)
```javascript
  //目前最常見也最方便
var person = {
    name:'duke',
    job:'java developer',
    sayName:function(){
        alert(this.name);
    }
};
  ```
#### 屬性存取
* 可以透過<strong> . </strong>來進行存取
```javascript
person.name; //duke
person.sayName();//duke
```
* 可以透過<strong>[ ]</strong>來進行存取，當key值為不合法的識別字(ex.空白或數字)會報錯
```javascript
person["name"]; //duke
person["sayName"](); //duke
person["001"] = 123;
person.001; //SyntaxError:Unexpected number
```
* 屬性新增：透過 = assign
* 屬性刪除：透過delete
```javascript
var obj ={};
obj.name = "joe";
obj.name; //joe
delete obj.name;
obj.sex; //undefined
```
#### 判斷屬性是否存在
* 存取不存在的屬性會回傳undefined
* in 運算子：除了檢查物件本身外，還會檢查物件的原型鏈(prototype chain)是否有該屬性
* hasOwnProperty()：只會檢查物件本身是否存在該屬性
```javascript
var obj ={name:'object'};
'name' in obj // true
'value' in obj // false

obj.hasOwnProperty('name'); // true
obj.hasOwnProperty('value'); // false
```
### 陣列Array
* 陣列內可以是基本型別 物件 函式等
* **有序集合**只能透過 [ ] 存取
#### 陣列建立
* 透過new
```javascript
var a = new Array();
a[0] = 1;
a[1] = 2;
a.length;
```
* 陣列實字(Array literal)
```javascript
var b = [];
b[0] = 1;
b[1] = 2;

var c = ['apple','banna'];
```
* Array.length 可被複寫：變長其他未賦予的會變成undefined，
```javascript
var array = ['james','tom']
array.length; // 2
array[4] = 'duke';
console.log(array); //['james','tom',undefined,undefined,'duke']
```
#### [Array常用API](https://developer.mozilla.org/zh-TW/docs/Web/JavaScript/Reference/Global_Objects/Array)
* push：加入項目至陣列最末端
* pop：移除陣列最末端
* unshift：加到陣列最前端
* shift：移除陣列最前端
#### 判斷是否為陣列
* Array.isArray()
## typeof
```javascript
typeof  true;         // 'boolean'
typeof  'duke';       // 'string'
typeof  123;          // 'number'
typeof  NaN;          // 'number'
typeof  { };          // 'object'
typeof  [ ];          // 'object'
typeof undefined;     // 'undefined'

typeof window.alert;  // 'function'
typeof null;          // 'object'
```
* 除了基本型別外的都是物件
* function實際上仍是物件，可以想成一種可以被呼叫的特殊物件
* null：JavaScript 的值是由一個表示「型別」的標籤，與實際內容的「值」所組合成的。由於物件 (Object) 這個型別的標籤是「0」，而且 null 代表的是空值 (NULL pointer，慣例上會以 0x00 來表示)，於是代表 null 的標籤就與物件的標籤搞混，而有著這樣錯誤的結果。
---

## [Day 05 JavaScript 是「傳值」或「傳址」？](https://ithelp.ithome.com.tw/articles/10191057)

### 變數相等
* Primitive
* Object 
```javascript
var a = 123;
var b = 123;
console.log(a === b); //true

var c = {value:123};
var d = {value:123};
console.log(c === d ); //false
```

### 變數的更新與傳遞
#### 更新
* Primitive
* Object
```javascript
var a = 123;
var b = a;
b = 10;
console.log(a); //123

var c = {value:123};
var d = c;
d.value = 10;
console.log(c); //10
console.log(c === d ); //true
```
#### 傳遞
* 結論：javascript是call by value 或稱call by sharing，相關可參考如下
* [深入探討 JavaScript 中的參數傳遞：call by value 還是 reference？](https://blog.techbridge.cc/2018/06/23/javascript-call-by-value-or-reference/)
  * 以 JavaScript 跟 Java 為例，在函式裡面重新賦值，外面的變數都不會變，所以就是屬於 pass by value，C++為例，會改變外面的變數，所以是call by reference。
* [[C/C++] 指標教學[四]: Pass by value vs Pass by reference](https://medium.com/@racktar7743/c-c-%E6%8C%87%E6%A8%99%E6%95%99%E5%AD%B8-%E5%9B%9B-pass-by-value-vs-pass-by-reference-ed5882802789)
---

## [Day 06 運算式與運算子](https://ithelp.ithome.com.tw/articles/10191180)
### [其他運算子MDN](https://developer.mozilla.org/zh-TW/docs/Web/JavaScript/Guide/Expressions_and_Operators)
### 算術運算子
#### 加號(+)
* 特殊數字
  * Infinity：Infinity - Infinity為NaN
  * NaN：其中一方為NaN則為NaN
* string
  * 其中一方為字串，另一方自動轉型為字串後連接在一起
  * number、boolean、object，轉型時會呼叫他們的toString()的「原型方法」去取得字串
  * null與undefined則是透過JavaScript的String()來轉型為"null"、"undefined"
  * 運算是計算由「左而右」且「先乘除後加減」
```javascript
-Infinity + Infinity; // NaN
10 + NaN; //NaN
true + 'abc'; //trueabc
100+{}; //100[object Object]

// 當數字與 undefined 相加時，undefined 會被嘗試轉成數字，也就是 NaN
123 + undefined     // NaN
"abc" + undefined   // "abcundefined"

// 當數字與 null 相加時，null 會被嘗試轉成數字，也就是 0
123 + null          // 123
"123" + null        // "123null"

//運算是順序
var a = 123;
var b = 123;
var str = "123 加 123 的數字會是" + a + b; //"123 加 123 的數字會是123123"
```
#### 減號(-)
* 特殊數字：同加號
* 基本型別：數字與其他基本型別，則JavaScript會先透過Number()嘗試為數字進行運算
* 物件型別：與物件型別的情況下，物件會先透過valueOf()的方法先求得對應的數值，若物件沒有valueOf()方法，則會先透過toString()轉成字串再以Number()嘗試轉為數值進行運算
```javascript
100 - "123"; //223
100 - "adsf"; //NaN
100 - true; //99
100 - undefined; // NaN
100 - null; //100
// object
100 -{}; //NaN
```
#### 乘號(*)
* 數值相乘：若超出範圍以Infinity或-Infinity表示
* 其中一個為NaN則為NaN
* 其中一非數字會以Number()進行轉換

#### 除號(/)
* 與乘號類似，其中一非數字會以Number()進行轉換
* 除數為0下
  * 被除數為0：Infinity
  * 被除數為負：NaN
  * 被除數為0：NaN

#### 餘數(%)
* 被除數是Infinity或-Infinity下取餘數都會是NaN
* 除數是Infinity或-Infinity下取餘數都會是被除數
* 與除法類似，其中一非數字會以Number()進行轉換
```javascript
Infinity % 0; //NaN
100 % Infinity; //100
```
