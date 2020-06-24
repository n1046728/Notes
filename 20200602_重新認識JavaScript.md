# 重新認識 JavaScript筆記
## Content  
>[Day 02 JavaScript 簡介](#day-02-javascript簡介)  
[Day 03 變數與資料型別](#day-03-變數與資料型別)  
[Day 04 物件、陣列及型別判斷](#day-04-物件陣列及型別判斷)  
[Day 05 JavaScript_是「傳值」或「傳址」？](#day-05-javascript-是傳值或傳址)  
[Day 06 運算式與運算子](#Day&nbsp;06&nbsp;運算式與運算子)  
[Day 07 「比較」與自動轉型的規則](#Day-07-比較與自動轉型的規則)  
[Day 08 Boolean 的真假判斷](#Day-08-Boolean-的真假判斷)  
[Day 09 流程判斷與迴圈](#Day-09-流程判斷與迴圈)  
[Day 10 函式 Functions 的基本概念](#Day-10-函式-Functions-的基本概念)  
[Day 11 前端工程師的主戰場：瀏覽器裡的 JavaScript](#Day-11-前端工程師的主戰場瀏覽器裡的-JavaScript)  
[Day 12 透過 DOM API 查找節點](#Day-12-透過-DOM-API-查找節點)  
[Day 13 DOM Node 的建立、刪除與修改](#Day-13-DOM-Node-的建立刪除與修改)  
[Day 14 事件機制的原理](#Day-14-事件機制的原理)  
[Day 15 隱藏在 "事件" 之中的秘密](#Day-15-隱藏在-"事件"-之中的秘密)  
[Day 16 那些你知道與不知道的事件們](#Day-16-那些你知道與不知道的事件們)  
[Day 17 函式裡的「參數」](#Day-17-函式裡的參數)  
[Day 18 Callback Function 與 IIFE](#Day-18-Callback-Function-與-IIFE)  
[Day 19 閉包 Closure](#Day-19-閉包-Closure)  
[Day 20 What's "THIS" in JavaScript (鐵人精華版)](#Day-20-Whats-THIS-in-JavaScript-鐵人精華版)  
[Day 21 函式的 Combo 技： Cascade](#Day-21-函式的-Combo-技-Cascade)  
[Day 22 深入理解 JavaScript 物件屬性](#Day-22-深入理解-JavaScript-物件屬性)  
[Day 23 基本型別包裹器 Primitive Wrapper](#Day-23-基本型別包裹器-Primitive-Wrapper)  
[Day 24 物件與原型鏈](#day-24-物件與原型鏈)    
[Day 25 原型與繼承](#day-25-原型與繼承)
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
---

## [Day 07 「比較」與自動轉型的規則](https://ithelp.ithome.com.tw/articles/10191254)

### 一元運算子
* 正號+與負號-  
  正號與負號後方帶的不是數值型態，則會先透過Number()進行轉型，物件型別則會透過物件的valueOf()先求得對應數值。有時會有人以+取代Number()進行轉型
  ```javascript
  var a = "10";
  console.log(-a); //-10

  var b = "helloworld";
  console.log(+b); //NaN

  +function(val){return val}; //NaN
  ```
* 遞增 ++ 與遞減 --  
  ```javascript
  var a = 10;
  var b = 10;
  console.log(a++); //10
  console.log(b++); //11
  console.log(a); //11
  console.log(b); //11
  ``` 
### 比較運算子(Comparison Operator)
* 「相等」== 與「全等」===  
  三個等號 === 與兩個等號 == 雖然都是比較的意思，但最大的差別在於「三個等號 === 不會替數值做自動轉型」。
  ```javascript
  false == 0; //true
  true == 1 ; //true
  [] == []; //false
  [] == ![]; // true

  var a = 10;
  var b = "10";
  console.log(a === b); //false
  ```
* 不等於!=與!==  
  概念同上

### 自動轉型規則
* 兩個都是數字，直接比較
* 字串與數字，字串會透過Number()嘗試轉型為數字後進行比較
* 其中一方為物件型別與基本型別，物件型別會透過valueOf()取得對應的基本型別後，再進行比較

### 數值的大於 > 與小於 <
* 兩個都是數字，直接比較
* 其中一個是數字，另一個則會試圖轉為數字再進行比較
* 兩者都是字串，則會按字母進行比較standard lexicolgraphical ordering
* 其中之一是boolean，則true看成1，false看成0
* 物件則透過valueOf()取得對應的值，若物件沒有valueOf()則透過toString()轉型再比較
* 
### [JS 真值表](https://thomas-yang.me/projects/oh-my-dear-js/)
---
## [Day 08 Boolean 的真假判斷](https://ithelp.ithome.com.tw/articles/10191343)
### 指派運算子(Assignment Operator)
| Operator | Actual |
| -------- | ------ |
| a+=b     | a=a+b  |
| a-=b     | a=a-b  |
| a*=b     | a=a*b  |
| a/=b     | a=a/b  |
| a%=b     | a=a%b  |

### 逗號運算子
分隔運算式可以循序執行(由左至右)並且回傳最後一個運算是值
* for loop
* 變數宣告
  ```javascript
  for(i = 0,j = 0;i<10;i++,j++){}

  var a =10,b = 10;
  ```
  ```javascript
  (function(){
    var a = b = 10; //注意此宣告會將b宣告為全域變數
    console.log(a,b);  
  })
  console.log(a,b); //undefined,10
  ```

### 邏輯運算子(Logical Operator)
> &&、||、!，有以上三種邏輯運算子，但非boolean遇到邏輯運算子時，會有兩種值，Falsy與Truthy。
#### Falsy 與 Truthy: 論 Boolean 的型別轉換
* Falsy
  > 經過ToBollean轉換為false的值：
  * undefined
  * Null
  * +0,-0,or Null
  * 空字串""或''
* Truthy
  > 其他轉換為true

#### 回到邏輯運算子
> &&、||、!
* 如果是Boolean類型就再做後續判斷，否則進行ToBoolean判斷falsy or truthy來轉換
* 對||來說，若是第一個數值轉換為true，則回傳第一個數值，否則回傳第二個數值
* 對&&來說，若是第一個數值轉會為true，則回傳第二個數值，否則回傳第一個數值
* if判斷式中javascript會針對回傳的數值在進行ToBoolean判斷是falsy或truthy
  ```javascript
  var a = 123;
  var b = 'abc';
  var c = null;

  console.log(a && b); //'abc'
  console.log(a || b); //123
  
  console.log(c && a); //null
  console.log(c || b); //abc
  ```
  ```javascript
  !!'false' == !!'true'; // true
  !!'false' === !!'true'; // true
  ```
  ---
## [Day 09 流程判斷與迴圈](https://ithelp.ithome.com.tw/articles/10191453)
### 條件語法(1) if...else
### 條件語法(2) switch
```javascript
var month = 12;
//Math.ceil(n) 無條件進位
//for loop
if(Math.ceil(month/3) === 1){
  console.log("spring");
}else if(Math.ceil(month/3) ===2 ){
  console.log("summer");
}else if(Math.ceil(month/3) === 3){
  console.log("fall");
}else if(Math.ceil(month/3 === 4)){
  console.log("winter");
}else{
  console.log("error month");
}

//switch
switch(Math.ceil(month/3)){
  case 1:
    console.log("spring");
    break;
  case 2:
    console.log("summer");
    break;
  case 3:
    console.log("fall");
    break;
  case 4:
    console.log("winter");
  default:
    console.log("error month");
    break;
}
```
#### switch注意事項
```javascript
//未使用break 造成異常
var m = 1;
switch(Month.ceil(m/3)){
  case 1:
    console.log("spring");
  case 2:
    console.log("summer");
  case 3:
    console.log("fall");
  case 4:
    console.log("winter");
  default:
    console.log("error month");
}
//spring
//summer
//fall
//winter
//error month

//適當使用break
var m = 1;
switch(m){
  case 1:
  case 2:
  case 3:
    console.log("spring");
    break;
  case 4:
  case 5:
  case 6:
    console.log("summer");
    break;
  case 7:
  case 8:
  case 9:
    console.log("fall");
    break;
  case 10:
  case 11:
  case 12:
    console.log("winter");
    break;
  default:
    console.log("error month");
}
```

### 三元運算子
(條件) ? [數值1] : [數值2]
```javascript
var status = age > 18 ? '成人' : '小孩';
```

### 迴圈
#### for loop
```javascript
for (var i = 0; i < 10; i++) {
  // 做某件事
}
console.log(i); //11，在java中會出錯
```
**注意變數i的有效範圍與for迴圈相同**

#### while loop
> 注意結束條件，以免無窮迴圈

#### break 與 continue
* break：回直接跳出迴圈
* continue：會跳過一次，然後繼續迴圈

#### for 與 while 兩者的差異點
* for loop：大多使用在明確狀態
* while：當迴圈使用在不確定次數時更適合
  ```javascript
  //大樂透1~49，選6個號碼
  var lottery = [];
  var n;
  while(lottery.length < 6){
    //random get num
    n = Math.floor(Math.random() * 49)+1;
    if(lottery.indexOf(n) === -1){
      lottery.push(n);
    }
  }
  ```
---
## [Day 10 函式 Functions 的基本概念](https://ithelp.ithome.com.tw/articles/10191549)
### Function
> 函式是物件的一種，除了基本型別以外的都是物件，可以想成是一種可以被呼叫(be invoked)的特殊物件
### 函式定義方式
* 函式宣告(Function Declaration)
* 函式運算式(Function Expressions)
* 透過**new Function**的關鍵字建立函式

#### 函式宣告
```javascript
function 名稱([參數]){
  //do something
}
```
#### 函式運算式
> 變數名稱 = function([參數]){...};，將一個函式透過=指定給某個變數
```javascript
var square = function (number){
  return number *number ;
}

//函式加入名字，只作用在自己的函式區塊內
var square = function func(number){
  console.log(typeof func); // function
  console.log(typeof square); //還是可以透過變數名稱取得function
  return number * number;
}
console.log(typeof func); // undefined
```
#### new Function關鍵字建立函式
>注意F大寫，透過new Function建立的函式，每次都會進行解析字串的動作，運作效能差，實務上較少這樣做
```javascript
var square = new Function('number','return number * number');
```

### 變數有效範圍(Scope)
> ES6以前**變數有效範圍最小的是以function做分界**，ES6 後有let與const他們的scope是透過大括號{ }來切分
[註2] ES6 之後有 let 與 const 分別定義「變數」與「常數」。 與 var 不同的是，它們的 scope 是透過大括號 { } 來切分的。
```javascript
var x = 1 ;
var doSomeThing = function(){
  var x = 100;
  return x+y;
}
console.log(doSomeThing(50)); //150
console.log(x); //1
```
```javascript
var x = 1 ;
var doSomeThing = function(){
  //內部找不到x就會到外部找，直到全域變數為止
  //都沒有就會報錯，ReferenceError:x is not defined
  return x + y;
}
console.log(doSomeThing(50)); //51
```
```javascript
var x = 1 ;
var doSomeThing = function(){
  x = 100; //沒有用var宣告
  return x+y;
}
console.log(x); //1
console.log(doSomeThing(50)); //150
console.log(x); //100
```
#### 變數拉升(Variable Hoisting)
>由於javascript有這樣的特性，強烈建議所有可能用到的變數都盡量在 scope 的最上面先宣告完成後再使用。
```javascript
var x = 1 ;
var doSomeThing = function(){
  console.log(x); //undefined 
  var x = 100;
  //以上Hoisting等同於
  // var x;
  //console.log(x);
  //x = 100;
  return x+y;
}
console.log(doSomeThing(50)); //150
console.log(x); //1
```
* 透過函式宣告的可以在宣告前使用(函式提升)
  ```javascript
  square(2); //4
  function square(num){
    return num * num;
  }
  ```
* 透過函式運算式會發生錯誤
  ```javascript
  square(2); //TypeError：square is not a function
  var square = function(num){
    return num * num;
  }
  ```
### 全域變數與區域變數
* 全域物件
  >javascript中沒有所謂全域變數，所以我們說的全域變數其實是全域物件(或叫頂層物件)，全域物件指的就是window，在node環境下叫做global
* 變數的有效範圍scope的最小切分為function(ES6中的let與const除外)
* 寫在函式內但沒有var的變數會變成全域變數
* 全域變數指的是全域物件(頂層物件)的屬性
  ```javascript
  var a = 10;
  console.log(window.a);// 10
  ```
---
## [Day 11 前端工程師的主戰場：瀏覽器裡的 JavaScript](https://ithelp.ithome.com.tw/articles/10191666)
### JavaScript與網頁前端的關係
* HTML：負責資料與結構
* CSS：負責樣式與呈現
* JavaScript：負責行為與互動

### 瀏覽器裡的JavaScript
> JavaScript未提供網頁的操作方法，前端網頁的操作方法是由JavaScript的執行平台「瀏覽器」所提供，這些操作方法由BOM、DOM這兩種物件所擁有

#### BOM
>BOM(Browser Object Model，瀏覽器物件模型)，是瀏覽器功能的核心

![BOMandDOM](imgs/BOMandDOM.png)

#### BOM的核心是**window**物件
* ECMAScript標準裡的「全域物件」(Global Object)
* JavaScript與瀏覽器溝通的窗口
* window物件提供主要的屬性參考上圖
* BOM提供很多API，可以直接操作瀏覽器，例如alert()警告對話框、confirm()、prompt()等
```javascript
// 全域作用範圍所宣告的變數 物件 函式都會式全域物件的屬性，
// 但「無法」使用delete來刪除
var a = 123;
console.log(window.a); //123
delete a ; //false
console.log(a); //123
```
```javascript
// 透過window屬性指定的，「可以」使用delete來刪除
var window.a = 123;
delete window.a; //true
console.log(window.a); //undefined
```
#### DOM
> DOM(Document Object Model，文件物件模型)，是一個將HTML文件以樹狀結構來表式的模型，組合起來的樹狀圖稱為DOM Tree
* 最根部為document
* DOM API就是定義了讓JavaScript可以存取與改變HTML架構、樣式與內容，以及節點事件綁定。  
  **範例：取得節點**
  ```javascript
  // 根據傳入的值，找到 DOM 中 id 為 'xxx' 的元素。
  document.getElementById('xxx');

  // 針對給定的 tag 名稱，回傳所有符合條件的 NodeList 物件 [註1]
  document.getElementsByTagName('xxx');

  // 針對給定的 class 名稱，回傳所有符合條件的 NodeList 物件。
  document.getElementsByClassName('xxx');

  // 針對給定的 Selector 條件，回傳第一個 或 所有符合條件的 NodeList。
  document.querySelector('xxx');
  document.querySelectorAll('xxx');

  /*[註1]: NodeList 物件是節點的集合，可藉由 Node.childNodes 屬性或 document.   querySelectorAll() 等方法取得。 NodeList 雖然有著與陣列相似的特性，但不是陣列，所以也不會有陣列相關的 method 可以使用 (如 map、filter 等)。
  */
  ```
  **範例：取得節點**
  ```html
  <h1 id="greet"></h1>

  <script>
    document.getElementById('#greet').textContent = "hello world";
  </script>
  ```
#### 「DOM」 與「BOM」的區別
* BOM：JavaScript與「瀏覽器」溝通的窗口，不涉及網頁內容
* DOM：JavaScript用來控制「網頁」的節點與內容的標準
---
## [Day 12 透過 DOM API 查找節點](https://ithelp.ithome.com.tw/articles/10191765)
> 當網頁載入瀏覽器時，瀏覽器會解析HTML檔案，依照HTML內容解析成「DOM」文件物件模型。DOM是W3C的制定的規範，獨立於平台與語言的標準，換言之，只要按照這樣的規範來實作，不管是什麼平台或語言開發，都可以透過DOM提供的API來操作DOM的內容、結構與樣式。

### 前言 script 標籤放哪有差別?
* 放在head tag之間
  >無法正確顯示HELLO，主要原因在於瀏覽器解析HTML檔案是「由上至下」依序解讀，此處在解析到head中的script時會暫停解析html而立刻去執行script直到執行完畢後再繼續解析網頁，由於此時尚未產生h1標籤，故無法取得
  ```html
  <!DOCTYPE html>
  <html>
    <head>
      <meta charset="utf-8">
      <script>
        document.getElementById("hello").textContent = "HELLO";
      </script>
    </head>
    <body>
      <h1 id="hello"></h1>
    </body>
  </html>
  ```
* 放在\<\/body>tag之前
  >下面範例成功顯示
  ```html
  <!DOCTYPE html>
  <html>
    <head>
      <meta charset="utf-8">
    </head>
    <body>
      <h1 id="hello"></h1>
      <script>
        document.getElementById("hello").textContent = "HELLO";
      </script>
    </body>
  </html>
  ```
### DOM 節點的選取
> document是DOM Tree的根節點，所以存取HTML時，都是從document物件開始，document節點類型如下
> * HTML元素節點(element nodes)
> * 文字節點(text nodes)
> * 註解節點(comment nodes)
```javascript
//常見的DOM選取方法

// 根據傳入的值，找到 DOM 中 id 為 'xxx' 的元素。
document.getElementById('xxx');

// 針對給定的 tag 名稱，回傳所有符合條件的集合
document.getElementsByTagName('xxx');

// 針對給定的 class 名稱，回傳所有符合條件的集合
// IE9 後開始支援
document.getElementsByClassName('xxx');

// 針對給定的 Selector 條件，回傳第一個 或 所有符合條件的 NodeList。
// IE8 後開始支援
document.querySelector('xxx');
document.querySelectorAll('xxx');
```
### DOM 節點的類型
>The read-only Node.nodeType property is an integer that identifies what the node is. 

 | 節點類型常數               | 對應數值 | 說明                                               |
 | :------------------------- | :------: | :------------------------------------------------- |
 | Node.ELEMENT_NODE          |    1     | HTML元素的Element節點                              |
 | Node.TEXT_NODE             |    3     | 實際文字節點，包括換行與空格                       |
 | Node.COMMENT_NODE          |    8     | 註解節點                                           |
 | Node.DOCUMENT_NODE         |    9     | 根節點                                             |
 | Node_DOCUMENT_TYPE_NODE    |    10    | 文件類型的DocumentType節點，例如HTML5的\<!DOCTYPE> |
 | Node_DOUMENT_FRAGMENT_NODE |    11    | DocumentFragment節點                               |
```javascript
document.nodeType === Node.DOCUMENT_NODE; //true
document.nodeType === 9 ; //true 
```
[MDN Node.nodeType ](https://developer.mozilla.org/en-US/docs/Web/API/Node/nodeType)

### DOM 節點間的查找遍歷 (Traversing)
* 父子關係
  >除document外，每一個節點都有個上層節點，稱為父節點(Parent node)，相對的下層節點稱為子節點(Child node)
* 兄弟關係
  >有同一個父節點稱，且在同一層，那麼他們彼此就是兄弟節點(Siblings node)

#### Node.childNodes
>The Node.childNodes read-only property returns a live **NodeList** of child nodes of the given element where the first child node is assigned index 0.
所有DOM節點物件都有childNodes屬性且此種屬性無法修改，我們可透過Node.hasChildNodes()來檢查某個DOM是否有子節點，可能的回值如下
* HTML元素節點(element nodes)
* 文字節點(text nodes)，包括空白
* 註解節點(comment nodes)

```javascript
var node = document.querySelector("#hello");
if(node.hasChildNodes()){
  //可以透過node.childNodes[n] 來取得對應節點
  //注意，NodeList物件內容為即時更新的集合
  for(var i = 0;i< node.childNodes[i];i++){
    ...
  }
}
```
#### Node.firstChild
>可以取得Node節點的**第一個**子節點，如果沒有子節點，則返回null
```html
<p id="test1">
  <span>span 1</span>
  <span>span 2</span>
  <span>span 3</span>
</p>

<p id="test2"><span>span 1</span><span>span 2</span><span>span 3</span></p>

<script>
  var p1 = document.getElementById("test1");
  var p2 = document.getElementById("test2");

  // tagName 屬性可以取得 node 的標籤名稱
  console.log(p1.firstChild.tagName);      // undefined
  console.log(p2.firstChild.tagName);      // SPAN
</script>
```
#### Node.lastChild
>可以取得Node節點的**最後一個**子節點，如果沒有子節點，則返回null

#### Node.parentNode
>可以用來取得父元素，回傳值可能會是(元素節點、根節點或DocumentFragment節點)
```html
<p>
    <span>span 1</span>
    <span>span 2</span>
    <span>span 3</span>
</p>

<script>
    var el = document.querySelector('span');
    console.log(el.parentNode.nodeName);    // "P"
    console.log(el.textContent); //span 1
</script>
```
#### Node.previousSibling
>可以取得同層之間的**前一個**節點，如果node已經是第一個節點，則返回null
```html
<p>
    <span>span 1</span>
    <span>span 2</span>
    <span>span 3</span>
</p>

<script>
    var el = document.querySelectorAll('span');
    console.log(el[0].previousSibling); // null
    console.log(el[2].previousSibling.textContext); //span 2
</script>
```
#### Node.lastSibling
>可以取得同層之間的下一個節點，如果該節點已經是最後一個，則返回null

#### document.getElementsBy**與document.querySelector/document.querySelectorAll差異
* document.getElementsBy** 回傳「HTMLCollection」
  >HTMLCollection只蒐集HTMLElement節點
* document.querySelectorAll 回傳「NodeList」
  >NodeList除了蒐集HTMLElement也包含屬性節點、文字節點等

**注意：**HTMLCollection/NodeList大部分情況下是**即時更新**的，但透過document.querySelector/document.querySelectorAll取得的NodeList是**靜態的**
```html
 <div id="outer">
        <div id="inner">
        </div>
    </div>
    <script>
        var el = document.querySelector('span');
        console.log(el.previousSibling);
        var el2 = document.querySelectorAll('span');
        for (var i = 0; i < el2.length; i++) {
            console.log("span:" + el2[i].textContent);
        }
        console.log("=============");
        var outDiv = document.getElementById("outer");
        var allDivs = document.getElementsByTagName("div");
        var allDivs2 = document.querySelectorAll('div');
        console.log(allDivs.length); //2
        console.log(allDivs2.length); //2
        outDiv.innerHTML = '';
        console.log(allDivs.length); //1
        console.log(allDivs2.length); //2
    </script>
```
---
## [Day 13 DOM Node 的建立、刪除與修改](https://ithelp.ithome.com.tw/articles/10191867)
### DOM節點新增
* document.createElement(tagName)
  >建立新HTML元素，在透過appendChild()、insertBefore()、replaceChild()等方法加入到指定位置才會顯示
* document.createTextNode()
  >建立文字節點的方法
  ```javascript
  //createElement
  var newDiv = document.createElement('div');
  newDiv.id ='myDiv';
  newDiv.className = 'box';

  //createTextNode
  var textNode = document.createTextNode('hello world');
  newDiv.appendChild(textNode);
  ```
* document.createDocumentFragment()
  >Node中DocumentFragment算是最特殊的一種，他是一種沒有父層節點的「最小文化物件」。可以把它看成輕量化的Document，如同標準文件一般方式來保存「片段的文件結構」。 
  * DocumentFragment與直接操作DOM最大的不同是DocumentFragment不是真實的DOM結構，所以DocumentFragment變動不會影響目前的網頁文件，也不會導致回流reflow或影響效能的情況
  * 當需要進行大量的DOM操作時，使用DocumentFragment效能會比DOM好很多
  ```html
  <ul id="myList"></ul>
  
  <script>
  var ul = document.getElementById('myList');
  var fragment = document.createFragment();

  for(var i =0;i<3;i++){
    let li = document.createElement('li');
    li.appendChild(document.createTextNode("Item "+(i+1)));
    fragment.appendChild(li);
  }
  ul.appendChild(fragment);
  </script>
  ```
* document.write()
  > document要將某內容寫入網頁可以使用write()方法，當頁面解析到document.write()時就會停下來，並且將內容輸出可以是字串也可以是HTML標籤
  ```javascript
  document.write("<h1>hello world!!</h1>");
  //<script type="text/javascript" src="file.js">
  document.write("<script type=\"text\javascript\" src="\file.js\">"+"<\/script>");
  ```
  ```javascript
  //window.onload表示網頁載入已完成後執行此function，無論網頁有什麼內容，都會被hello world取代
  window.onload = function(){
    document.write("hello world");
  }
  ```
### DOM節點的修改與刪除
* Node.appendChile(childNode)
  >加入到父容器節點的末端
* Node.insertBefore(newNode,refNode)
  >將新節點加入到refNode節點的前面
* Node.replaceChild(newChildNode,oldChildNode)
  >將原本的oldChihld由newChild取代  
* Node.removeChild(childNode)
  >將指定的childNode移除
```html
<ul id="myList">
  <li>item 1</li>
  <li>item 2</li>
  <li>item 3</li>
</ul>

<script>
  var myList = document.getElementById('myList');
  var newListItem = document.createElement('li');
  var textNode = document.createTextNode("hello world!!");
  newListItem.appendChild(textNode);
  myList.appendChild(newListItem);

  //insertBefore
  var refNode = document.querySelectorAll('li')[1];//取得item 2的節點
  myList.insertBefore(newListItem,refNode);
  //replaceChild
  var oldNode = document.querySelectorAll('li')[0]//取得item 1的節點
  myList.replaceChild(newListItem,oldNode);
  //removeChild
  var removeNode = document.querySelectorAll('li')[0]//取得第一個節點
  myList.removeChild(removeNode);
</script>
```
---
## [Day 14 事件機制的原理](https://ithelp.ithome.com.tw/articles/10191970)
>JavaScript是一個事件驅動(Event-driven)的程式語言，當瀏覽器載入網頁開始讀取後雖然會馬上讀取到JavaScript事件相關的程式碼，但必須等到事件(user點擊、按下鍵盤)被觸發，才會進行對應程式的執行。而「點擊按鈕
」就被稱為**事件(Event)**，負責處理事件的程式稱為「**事件處理者**」(**Event Handler**)
### 事件流程Event Flow
>事件流程(Event Flow)指的是**網頁元素接收事件的順序**
* 事件冒泡(Event Bubbling)
  >事件冒泡指的是「從啟動元素的節點開始，逐層往上傳遞」，直到整個網頁的根節點，也就是**document**

  ![bubblePhaseImg](imgs/BubblePhase.png)
* 事件捕獲(Event Capturing)
  >事件捕獲與事件冒泡的傳遞順序相反

  ![capturePhaseImg](imgs/CapturePhase.png)
* Event Flow
  >事件傳遞有兩種機制，事件兩種都會執行，此處以點擊td為例

  ![EventFlowImg](imgs/EventFlow.png)
* 檢驗事件流程
  ```html
  <div id="parent">
    父元素
    <div id="child">子元素</div>
  </div>
  ```
  ```javascript
  var parent = document.getElementById('parent');
  var child = document.getElementById('child');
  // 透過 addEventListener 指定事件的綁定
  // 第三個參數 true / false 分別代表捕獲/ 冒泡 機制

  parent.addEventListener('click', function () {
    console.log('Parent Capturing');
  }, true);

  parent.addEventListener('click', function () {
    console.log('Parent Bubbling');
  }, false);

  child.addEventListener('click', function () {
    console.log('Child Capturing');
  }, true);

  child.addEventListener('click', function () {
    console.log('Child Bubbling');
  }, false);
  ```
  點擊子元素，則觸發順序，而子層的Bubbling、Capturing觸發順序(按程式碼順序而定)
  ```javascript
  "Parent Capturing"
  "Child Capturing" //child capturing 、child bubbling是程式碼順序而定
  "Child Bubbling"
  "Parent Bubbling"
  ```
  點擊父元素，則
  ```javascript
  "Parent Capturing"
  "Parent Bubbling"
  "Child Capturing" //按程式碼順序亦可能先Child Bubbling、Child Capturing
  "Child Bubbling"
  ```
### 事件的註冊綁定
* on-event 處理器 (HTML 屬性)
  >對HTML元素來說只要支援某個事件的觸發，可以透過on+事件名的屬性來註冊，但基於程式碼使用性與維護性的考量，不建議以此方式綁定，參考wiki[非侵入式JavaScript](https://zh.wikipedia.org/wiki/%E9%9D%9E%E4%BE%B5%E5%85%A5%E5%BC%8FJavaScript)
  ```html
  <button id="btn" onclick="console.log('hello');">Click</button>
  ```
* on-event 處理器 (非 HTML 屬性)
  >像window與document沒有實體元素，我們可以透過DOM API提供的on-event處理器(on-event handler)來處理，實體元素可透DOM API取得DOM後透過on-event handler處理
  ```javascript
  window.onload = function(){
    document.write("hello world");
  };
  
  var btn = document.getElementById('btn');
  btn.onclick = function(){
    console.log("hello");
  };
  ```
  #### 解除事件
  ```javascript
  btn.onclick = null;
  ```
* 事件監聽 EventTarget.addEventListener()
  >有三個參數分別是「事件名稱」「事件的處理器(觸發執行的function)」「Boolean(決定冒泡或捕獲，default為冒泡)」，此種方式的優點是可以重複指定多個處理器(handler)給同一個元素的同一個事件
  ```html
  <button id="btn">Click</button>

  <script>
    var btn = document.getElementById('btn');

    btn.addEventListener('click', function(){
      console.log('HI');
    }, false);

    btn.addEventListener('click', function(){
      console.log('HELLO');
    }, false);
  </script>
  ```
  點擊後出現
  ```javascript
  "HI"
  "HELLO"
  ```
  #### 解除事件removeEventListener()
  >參數解釋同addEventListener()，但須注意第二個參數handler必須與先前addEventListener的handler同一個實體
  ```javascript
  var btn = document.getElementById('btn');
  // 把 event handler 拉出來
  var clickHandler = function(){
    console.log('HI');
  };
  
  btn.addEventListener('click', clickHandler, false);
  // 移除 clickHandler， ok!
  btn.removeEventListener('click', clickHandler, false);
  ```                                                             
---
## [Day 15 隱藏在 "事件" 之中的秘密](https://ithelp.ithome.com.tw/articles/10192015)

### 隱藏在 Handler 中的 "event"
> 當監聽事件發生的時，瀏覽器會去執行們透過addEventListener()註冊的EventHandler(EvenListener)，也就是我們指定的function。此時EventListener會去建立一個「事件物件」Event Object，裡面包含這個事件有關的屬性，並以「參數」的形式傳給EventHandler
```html
<button id="btn">Click</button>
```
```javascript
var btn = document.getElementById("btn");
btn.addEventListener('click',function(e){
  console.log(e);
},false);
```
* type：表示事件名稱
* target：表示觸發事件元素
* bubbles：表示事件是否在冒泡階段觸發(true/false)
* pageX/pageY：觸發事件時滑鼠座標在網頁的相對位置

### 阻擋預設行為event.preventDefault()
> HTML部分元素有預設行為，例如\<a>的連結，或是表單的submit()等等，如果我們需要在這些元素上綁定事件，適時**取消他們的預設行為**是一件很重要的事
```html
<a id='link' herf='https://www.google.com'> Google</a>
```
綁定click事件，阻止a的預設行為，前往google網站
```javascript
var link = document.querySelector('#link');
link.addEvenListener('click',function(e){
  e.preventDefault(); //或是function結尾加入return false;
  console.log('google');
},false);
```

### 阻擋事件冒泡傳遞(event.stopPropagation())
常用情境：一般增強checkbox的易用性，通常會增加一個label標籤，然後for屬性給對應的label

```html
<label for="xxx">Label2</label>
  <input type = "checkbox" name="chkbox" id="xxx">
<!-- 有時因需求不想給太多id 也會寫成以下形式，也有一樣的效果 -->
<label class="lbl">
  Label <input type="checkbox" name="chkbox">
</label>
```
```javascript
var lbl = document.querySelector('.lbl');
lbl.addEventListener('click',function(e){
  console.log("lbl click");
},false);
```
點選label會發現，console.log("lbl click")被觸發兩次，發生這樣的問題是因為\<label>包覆checkbox，當點擊label觸發click事件，瀏覽器又將click事件帶給checkbox，而checkbox受事件冒泡影響又再度把事件傳遞給label上導致"lbl click"出現兩次
```html
<label class='lbl'>
  <input type="checkbox" name="chkbox" id="chkbox">
</label>

```
```javascript
var lbl = document.querySelector('.lbl');
var chkbox = document.getElementById('chkbox');
lbl.addEventListener('click',function(e){
  console.log("lbl click");
},false);
chkbox.addEventListener('click',function(e){
  console.log("chkbox click");
  //若要避免2次lbl click，可在此處加入e.stopPropagation
  //e.stopPropagation();
},flase)
```
result：
```javascript
"lbl click"
"chkbox click"
"lbl click"
```
#### 注意
* stopPropagation需放在checkbox才會有效
* jquery的EventHandler最後加上return false;可達到preventDefault()、stopPropagation()的效果
* javascript的addEventListener()最後加入return false沒有上述作用，只有在onClick="return false"的情況下才有作用

### 在事件中找回「自己」
> 當事件觸發，此時this就是觸發事件的元素，以上例來說就是label  
注意：this代表的是「事件觸發的**目標**」，也就是event.currentTarget而不是e.target

html同上
```javascript
//label 
var lbl = document.querySelector('.btn');
var chkbox = document.querySelector('#chkbox');

lbl.addEventListener('click',function(e){
  console.log(e.target.tagName,1);
  console.log(this.tagName,1);
},false);

chkbox.addEventListener('click',function(e){
  console.log(e.target.tagName,2);
  console.log(this.tagName,2);
},false);
```
按下label觸發click後，result
```javascript
"LABEL 1"
"LABEL 1"
"INPUT 2"
"INPUT 2"
"INPUT 1"
"LABEL 1"
```
* e.target：是觸發事件的元素
* this是指觸發事件的目標元素，也就是event.currentTarget

### 事件指派(Event Delegation)
>是指利用前面介紹的事件流程及單一監聽事件來處理多個事件目標
#### 原始作法
```html
<ul id="myList">
  <li>item 1</li>
  <li>item 2</li>
  <li>item 3</li>
</ul>
```
```javascript
var myList = document.getElementById('myList');
if(myList.hasChildNode()){
  for(var i = 0;i< myList.childNodes.length ; i++){
    //nodeType ===1 代表實體html元素
    if(myList.childNodes[i]).addEventListener('click',function(e){console.log(this.textContent)},false);
  }
}
```
此時，若要新增元素至myList，則新節點並不會有click事件註冊，而且是我們不斷的去重複監聽事件，又忘了移除監聽，可能造成memory leak的情形
#### 事件指派(Event Delegation)
> click事件由外層的myList來監聽，利用事件傳遞的原理，判斷e.target目標節點時才做動作
```javascript
var myList = document.getSelector("#myList");
myList.addEventListener('click',function(e){
  if(e.target.tagName.toLowerCase() === 'li'){
    console.log(e.target.textContext);
  }
},false);

//就算加入新元素也有監聽到
var newListItem = document.createElement('li');
var textNode = document.createTextNode("hello ");
newListItem.appendChild(textNode);
myList.appendChild(newListItem);
```
---
## [Day 16 那些你知道與不知道的事件們](https://ithelp.ithome.com.tw/articles/10192175)

### 事件的種類
  * 介面相關事件
    >介面相關事件不一定會與使用者對DOM的操作有關係，反而大多與window物件比較相關
    * load
      >註冊在window物件上，指的是網頁資源(包括CSS JS 圖片等)全數載入後觸。  
       如果是img元素的load事件，則表示圖片載入後觸發。
    * unload、beforeload
      >事件分別會在離開頁面或是重新整理的時候觸發，而beforeload會跳出對話框詢問使用者是否要離開目前頁面。
    * error事件
      >error事件會在document或圖片載入錯誤時觸發，值得一提的是，由於維護性的考量，大多是件會建議使用非侵入式的JavaScript的寫法，另外寫在\<script>標記，只有error事件最適合寫在on-event handler的寫法來處理
      ```html
      <img src="image.jpg" onerror="this.src='default.jpg'">
      ```
      **注意**：若是網頁在load事件完才註冊error事件的hanler，只會看到叉燒包或破圖的結果，因為error事件不會再被觸發，後來掛上的handler也一樣
    * resize事件：當瀏覽器(window)或指定元素(element)的尺寸變更時觸發
    * scroll事件：當瀏覽器(window)或指定元素(element)的捲軸被拉動時觸發
    * DOMContentLoaded事件
      >類似於load事件，load事件是「所有」資源都已經被載入完成後才會觸發，而DOMContentLoaded事件是在DOM結構完整的讀取跟解析後就會觸發，不需等外部資源讀取完成
      ![DOMContentLoadedImg](imgs/DOMContentLoaded.png)

      解決script放在head中讀不到的問題
      ```html
      <head>
        <script>
          document.addEventListener('DOMContentLoaded',function(e){
            document.getElementById('hello').textContent = "hello world!";
          },false)
        </script>
      </head>
      <body>
        <div id='hello'></div>
      </body>
      ```
  * 滑鼠相關事件
    >滑鼠相關事件都可以透過event.pageX與event.pageY取得網頁對應的座標
    * mousedown / mouseup事件
      >這兩個事件分別會在滑鼠點擊了某個元素「按下」(mousedown)按鈕，以及「放開」(mouseup)按鈕時觸發
    * click事件：滑鼠點擊某元素時觸發
    * dbclick事件：當滑鼠連點兩次某元素時觸發
    * mouseenter / mousemove / mouseleave事件  
      1.當滑鼠移入某個元素時，會先觸發mouseenter是件  
      2.滑鼠游標在某個元素中「移動」時，會連續觸發mousemove  
      3.滑鼠游標離開了這個元素時，才會觸發mouseleave
  * 鍵盤相關事件
    >大多會將鍵盤的事件建立在input的輸入框上
    * keydown事件：「壓下」鍵盤按鍵時會觸發
    * keypress事件：除了shift Fn CapsLock這三種按鍵按住時會觸發，按著不放會連續觸發
    * keyup事件：「放開」按鍵時觸發  
    對同一元素綁定三個事件時執行順序：
      ```javascript
      "keydown"
      "keypress"
      "keyup"
      ```
    **注意：**若想知道使用者按下的按鍵可透過event.keyCode屬性來查詢，[KeyCode對應表](https://gist.github.com/tylerbuchea/8011573)

  * 表單相關事件
    * input事件：當input textarea以及帶有contenteditable的元素內容被改變時觸發
    * change事件
      >當input select  textarea radio checkbox等表單內容被改變時觸發，與input事件不同的是，input事件會在輸入框輸入的當下觸發，而change事件則是目前焦點離開輸入框後才觸發
    * submit事件：當表單被送出時觸發，通常表單驗證都會在這一步處理，若驗證未通過則return false;
    * focus事件：當元素被聚焦時觸發
    * blur事件：當元素失去焦點時觸發

  * 特殊事件
    * Composition Event(組成事件)：
    >Composition Event是指compositonstart、compositionend以及compositionupdate，像在google的搜尋框，會用autocomplete(自動完成)的方式給使用者搜尋建議，輸入中文時，通常會透過注音相關的輸入法做輸入，大部分情況針對注音符號、拼音文字去給搜尋建議沒有太大意義，這個時候需要透過Composition Events來為輸入框做加強，透過Composition Events可以觀察使用者在輸入框開啟輸入法(Input Method Editor，IME)時，字組或選字狀態
    * compositionstart：輸入框內開啟輸入法，且**正在拼字時**觸發
    * compositionupdate：輸入框內開啟輸入法，且**正在拼字**或**選字時**更改了內容時觸發
    * compositionend：輸入框內開啟輸入法，拼字或選字**完成**，正要送出至輸入框時觸發
  
  * 自訂事件
    >自訂事件可以用Event Constructor建立，同樣透過addEventListener去監聽，由dispatch決定觸發的時機
    ```javascript
    var event = new Event('build');
    //監聽
    elem.addEventListener('build',function(e){...},false);
    //觸發
    elem.dispatchEvent(event);
    ```
    若想要在自訂事件增加更多資料，可透過CustomEvent
    ```javascript
    var event = new CustomEvent('build',{'detail':elem.dataset.time})
    ```
    那麼在eventHandler就可透過event來接收
    ```javascript
    function(e){
      console.log(e.detail);
    }
    ```
---
## [Day 17 函式裡的「參數」](https://ithelp.ithome.com.tw/articles/10192368)
### 一級函式(First class functions)
> 一級函式指的是你可以將函式存在變數、物件以及陣列之中，同時也可以將函式傳到函式，或由另一個函式來回傳，而且函式具有屬性，因為它實際上是一個「物件」。
```javascript
//把函式存到「變數」，呼叫時執行funcA()
var funcA = function(){console.log("hello world")};
//把函式存到「陣列」，呼叫時執行funcB[0]()
var funcB = [funcA]
//把函式存到「物件」屬性中，呼叫時執行funcC.method()
var funcC = {method:funcA}
```
```javascript
//把函式當作「參數」傳到另一個函式中
var funcD = function(func){
  return func;
};
//另一個函式：存放的是funcD，而參數是一個匿名函式
var runFuncPassedToFuncD = funD(function(){console.log('Hi!')});
//呼叫另一個函式
runFuncPassedToFuncD(); //Hi!
```
```javascript
var funcE = function(){};
funcE.answer = 'yaya';
console.log(funcE.answer); //yaya
```

### 函式裡的參數
>呼叫一個函式時，可以透過「函式名稱」加上小括號的方式，括號內的資料就是「參數」
```javascript
var plus = function(numA,numB){return numA+numB;};
plus(1,2); //3
plus(2,3); //5
```
>定義函式時有指定的參數數量，但是呼叫時並不會對帶入的參數進行檢查，而沒有指定的參數預設會是**undefined**
```javascript
plus(1,2,3,4,5);
plus();// numA,numB 為undefined
```
### arguments物件
>函式被呼叫時，會產生一個arguments物件，此物件的內容就是傳入的參數。arguments並非「陣列」，但他只是帶有索引特性的物件，內件length屬性，其他與陣列完全不同，沒有.map()或.filter()方法，但仍然可以透過 slice 或是 ES6 的 Array.from 來將它轉成一個新的陣列。
```javascript
var plus = function(numA,numB){
  console.log(arguments.length);
  for(var i = 0;i<arguments.length;++){
    console.log(i);
  }
  return numA + numB;
};
plus(1,2,3,4,5) 5 1 2 3 4 5 3
```
> argument的另一個屬性callee，指的是目前執行的函式，當我們在函式執行「遞迴」時，可以執行arguments.callee()來達成，這個函數在匿名函式特別有用。但要小心「嚴格模式」下不允許存取arguments.caller與arguments.callee這兩個屬性
```javascript
var plus = function(numA,numB){
  console.log(arguments.callee)};
  return numA + numB;
```
>ES6 的箭頭函式(Arrow Funciton)沒有提供arguments物件

### 以「物件」為參數
>**將多個參數用「物件」包裝起來**，當遇到函式參數一大堆「**順序不能錯，參數不能漏**」，此時用物件來包裝就會很方便
```javascript
var addPerson = function(firstName,lastName,phone,email,gender,birthday,address){....}
addPerson('james','syu','091234556','abc@gmail.com','male','1900-1-1','XXXXXX');
var person = {
  firstName:'james',
  lastName:'syu',
  phone:'091234556',
  email:'abc@gmail.com',
  gender:'male',
  birthday:'1900-1-1',
  address:'XXXXXX'
}
//將person作為參數傳入
addPerson(person);
```
### 參數的預設檢查
>當函式傳少了的那些值會變成undefined，此時就需要對函式進行檢查，可以透過||(OR)運算子來處理
```javascript
var plus = function (numA, numB) {
  numA = numA || 0;
  numB = numB || 0;

  return numA + numB;
};
```
>被判斷成false的值不只undefined，更嚴謹的寫法
```javascript
var plus = function (numA, numB) {
  numA = (typeof numA !== 'undefined') ? numA : 0;
  numB = (typeof numB !== 'undefined') ? numB : 0;

  return numA + numB;
};
```
>ES6 可以替參數指定預設值
```javascript
var plus = function(numA=0,numB=0){return numA+numB};
```
---
## [Day 18 Callback Function 與 IIFE](https://ithelp.ithome.com.tw/articles/10192739)
### Callback Function
>Callback Function與一般函式沒有什麼不同，差別在於呼叫執行的時間。函式只會在滿足了某個條件才會被動的去執行，其實就是「**把函式當另一個函式的參數，透過另一個函式來呼叫它**」。  

> 「JavaScript是一個事件區發的(Event-driven)的程式語言」，概念如同：  
> 辦公室電話響(事件被觸發Event fired) -> 接電話(Event Handler) 
```javascript
Office.addEventListener('電話響',function(){/*接電話*/},false);
```
### 把函式當作另一個函式的參數
>希望隔某段時間，執行某件事可以透過window.setTimeout來達成
```javascript
// 1000 millisecond = 1 second
window.setTimeout(function(){},1000); 
```
>使用場景：「**控制多個函式間的執行順序**」
```javascript
var funcA = function(){
  console.log("funcA");
};
var funcB = function(){
  console.log("funcB");
}

funcA();
funcB();
/*result：
  funcA
  funcB
*/
```
>加上一個隨機生成時間，此時無法確定執行先後
```javascript
var funcA = function(){
  var i = Math.random()+1;
  window.setTimeout(function(){
    console.log("funcA");},i*1000);
};
var funcB = function(){
  var i = Math.random()+1;
  window.setTimeout(function(){
    console.log("funcB");},i*1000);
};

funcA();
funcB();
```
>確保執行順序，使用callback function形式來處理，但須注意callback多層之後產生的「波動拳」(a.k.a "CallbackHell")
```javascript
//確保先執行funcA在執行funcB，在funcA中加入callback參數
var funcA = function(callback){
  var i = Math.random()+1;
  window.setTimeout(function(){
    console.log("funcA");
  },i*1000);
  if(callback typeof 'function'){
    callback();
  };
};

var funcB = function(){
  var i = Math.random()+1;
  setTimeout(function(){
    console.log("funcB");
  },i*1000);
};

funcA(funcB);
```
### 立即被呼叫的函式(Immediately Invocked Function Expression,IIFE)
> 記住JavaScript變數有效範圍的最小單位是以**function**切分
```javascript
for(var i = 0;i<5;i++){
  window.setTimeout(function(){
    console.log(i);
  },1000)
};
```
>執行結果，console.log在「一秒鐘之後」，同時印出「五次5」 
```javascript
5
5
5
5
5
```
>原因：  
JavaScript是一個「非同步」的語言，所以在執行程式時，for迴圈並不會等待window.setTimeout執行完才繼續，而是執行階段**一口氣**跑完  
第0秒時：for迴圈已將五次的setTimeout()執行完  
第1秒時：function去外層拿取變數i時已經是5，console.log()會在一秒鐘之後印出「五次5」  

>兩個問題待解決：-> 立即被呼叫的特殊函式(IIFE)
1. console.log印出的順序
2. console.log執行時間

>IIFE
```javascript
// 函式宣告下即呼叫
(function doSomething(i){
  //do something
};)(123); //加一個括號直接執行呼叫

//函式也可以不取名
(function(i){
  //do something
};)(222);
```
>Q1 solution：切分變數的有效範圍的最小單位是function，每次迴圈將i傳給內部function保存，不過下述範例for迴圈一次跑完window依序註冊五次timer，所以每個timer等待一秒鐘，同時將變數印出
```javascript
for(var i = 0;i<5;i++){
  //為凸顯差異，將傳入後的參數名改為x
  //當然因scope的不同，繼續沿用i也是可以
  (function(x){
    window.setTimeout(function(){
      console.log(x);
    },1000);
  };)(i);
};

//result:0 1 2 3 4
```
>Q2 solution：修改內部迴圈等待時間
```javascript
for(var i = 0;i<5;i++){
  //為凸顯差異，將傳入後的參數名改為x
  //當然因scope的不同，繼續沿用i也是可以
  (function(x){
    //將1000 改成1000*x
    window.setTimeout(function(){
      console.log(x);
    },1000 * x);
  };)(i);
};

//result:0 1 2 3 4
```
> IIFE小結：
> * 迴圈內呼叫function時，可以利用IIFE來參數值保存下來
> * 減少全域變數的產生，同時避免變數名稱衝突的機會
> ES6後新增的let與const可以做，且改以{}作為scope，所以可以保留迴圈當下的值
```javascript
for(let i = 0 ;i<5;i++){
  window.setTimeout(function(){
    console.log(i);
  },1000);
};
```
> 備註：不了解作者寫的，「如果你有去看過 jQuery 的原始碼，就會發現 jQuery 也用了相同的手法將 window 與 undefined [註2] 保留起來：」
```javascript
(function( window, undefined ) {

  // 略...

})( window );
```
---
## [Day 19 閉包 Closure](https://ithelp.ithome.com.tw/articles/10193009)
### 範圍鏈Scope Chain
> 「切分變數有有效範圍的最小單位是"function"」。如下範例，內層的function inner可以讀取外層宣告的變數，但外層的outer function存取不到內層宣告的變數。若是在自己的層級找不到就會一層一層往外找，最後找到Global為止。這種行為就稱為「範圍鏈」

```javascript
function outer(){
  //outer層拿不到變數c
  //但可以向外找到變數的a
  //注意如果沒有var宣告b將成為全域變數
  var b = a * 2;

  function inner(c){
    //雖然只有宣告c，但因為範圍鏈，所以可以存取到a,b
    console.log(a,b,c);
  };
  inner(b*3);
};
//global 層只有a，不認得b,c
var a = 1;
outer(a);
```
>測驗
```javascript
var msg = 'global.';
function outer(){
  var msg = 'local.';
  function inner(){
    return msg;
  };

  return inner; //此處回傳的是這個function的參考並非呼叫，呼叫是inner() 
};

var innerFunc = outer(); //此處是將outer()回傳的結果給innerFunc，也就是inner function的參考
var result = innerFunc();//此處innerFunc()會呼叫inner()將回傳結果給result
console.log(result); // local.
```
### 閉包Clousure
>當內部(inner)函式被回傳後，除了自己本身的程式碼外，也可以取得內部函式「當時環境」的變數值，記住了當時環境，這就是「閉包」

>此處IIFE，廣義來說也是儲存閉包的作法，執行setTimeout的同時會將變數i鎖起來，延續它的生命
```javascript
for(var i =0;i<5;i++){
  (function(i){
    window.setTimeout(function(){
      console.log(i);
    },1000 *i);
  })(i);
}
```
>計數器範例
* 沒有使用閉包：使用全域變數儲存count
  >當程式碼變多，過多全域變數會造成不可預期的錯誤，像是與同事間的變數名衝突、沒用到的變數無法回收等
  ```javascript
  var count =0;
  function counter(){
    return ++count;
  };

  console.log(counter()); //1
  console.log(counter()); //2
  console.log(counter()); //3
  ```
* 使用閉包
  ```javascript
  function counter(){
    var count = 0;
    function innerCounter(){
      return ++count;
    };
    return innerCounter;
  }
  var countFunc = Counter();
  console.log( countFunc() ) //1
  console.log( countFunc() ) //2
  console.log( countFunc() ) //3
  ```
  >進一步簡化
  ```javascript
  function counter(){
    var count = 0;
    return function(){
      retrun ++count;
    };
  };
  ```
  >ES6箭頭函數簡化(Arrow Function)
  ```javascript
  function counter(){
    var count = 0;
    return () => ++count;
  };
  ```
  >新增另一個計數器，閉包寫法將是兩個「獨立」計數器實體，彼此互不干擾
  ```javascript
  function counter(){
    var count =0;
    return function(){
      return ++count;
    }
  };

  var countFunc = counter();
  var countFunc2 = counter();

  console.log(countFunc()); //1
  console.log(countFunc()); //2
  console.log(countFunc2()); //1
  console.log(countFunc2()); //2
  ```
---
## [Day 20 What's "THIS" in JavaScript (鐵人精華版)](https://ithelp.ithome.com.tw/articles/10193193)

### What's this?
> 在其他物件導向中，你會知道它會指向某的建構子(Constructor)所建立的物件。JavaScript裡，this所代表的不僅是那個被建立的物件
* this是JavaScript的關鍵字
* this是function執行時，自動生成的一個內部物件
* 隨著function執行場合不同，this所指向的值，也會有所不同
* 大多數情況下，this代表的就是呼叫function的物件(Owner Object of the function)
```javascript
var getGender = function(){
  return this.gender;
};

var people1 = {
  gender :'female',
  getGender:getFender
};

var people2 = {
  gender :'male',
  getGender:getFender
};

console.log(people1.getGender()); //female
console.log(people2.getGender()); //male
```
### this不等於function
> this 代表的是function執行時所屬的物件，而不是function本身。

>此在for迴圈中執行的foo()中的this指的是window，由於window.count並未定義，為undefined，執行迴圈後會得到NaN的結果
```javascript
var foo = function(){
  this.count++;
};

foo.count = 0;
for(var i =0;i<5;i++){
  foo();
};

console.log(foo.count); // 0
console.log(window.count) //NaN
```
>另一個範例，bar、foo皆為window所有，此處的this.a也就是指window.a，由於未定義，所以為undefined
```javascript
var bar = function(){
  console.log(this.a);
};
var foo = function(){
  var a = 123;
  this.bar();
};

foo();
```
### 巢狀迴圈中的this
> * JavaScript中，用來切分變數的最小作用範圍(scope)，也就是說有效範圍的單位是function
> * 當沒有指名this的情況下，預設綁定(Default Binding)this就是「全域物件」window
```javascript
var obj = {
  func1 : function(){
    console.log(this === obj); // true
    var func2 = function(){
      //此處的this 指的是window 
      console.log(this === obj); // false
    }; 
  };
};
```
>ES5的嚴格模式下，會禁止this指定為全域物件
```javascript
var obj = {
  func1 : function(){
    "use strict";
    console.log(this === obj); // true
    var func2 = function(){
      //宣告成嚴格模式後，此處就會變undefined 
      console.log(this); // undefined
    }; 
  };
};
```
### That or This?
> 要是我們在callback function加入ajax請求，依據前述，default binding會把這個callback function的this指定給global object，也就是window，解決方式透過另一個參數來對目前的this做參考
```javascript
el.addEventListener('click',function(){
  //透過that參考
  var that = this;
  console.log(this.textConent);
  $ajax('[URL]',function(res){
    //this.textContent =>undefined
    console.log(that.textContent,res);
  });
},false);
```
### 強制指定this的方式
> javascript有三個可以強制指定的this的方式，分別是bind()、call()、apply()
#### .bind()
```javascript

el.addEventListener('click',function(){
  //透過.bind(this) 來強制指定該scope的this
  console.log(this.textConent);
  
  $ajax('[URL]',function(res){
    console.log(that.textContent,res);
  }).bind(this);
},false);
```
```javascript
var obj = {
  x : 123;
};
var func = function(){
  console.log(this.x);
};
func(); //undefined
func().bind(obj); //123
```
#### 箭頭函式與this
> 箭頭函式的兩個重要特性，更簡短的函式寫法、this變數強制綁定。但須注意，無論使用'use strict'或再加上.bind()都無法改變this的內容，也不能作為物件建構子(constructor)來使用。Arrow function也需注意，若function內需要用到this的情況時，須留意this是否換人來當
```javascript
el.addEventListener('click',function(){
  //Arrow function 強制指定this至callback function中
  $ajax('[URL]',res => {
    console.log(this.textContent,res);
  });
},false);
```
#### .call()與.apply()
> .call與.apply()都是呼叫函數執行，並**將這個function的context替換成第一個參數帶入的物件**，例如強制指定某物件為該function執行時的this。call與apply只差別在於**傳遞方式**有所不同
```javascript
function func(){
  // do something
};

//呼叫方式
func();
func().call();
func().applu();
//參數傳遞
function funcA(arg1,arg2,arg3,....){
  //do something
};

funcA.call(context,arg1,arg2,arg3,....);
funcA.apply(context,[arg1,arg2,arg3,....]); //陣列為參數
```
#### bind,call,apply的差異
>bind()讓這個function在呼叫前先綁定某個物件，使他不管怎麼呼叫都能有固定的this。例如使用在callback function的場景。而call與apply則是使用在context較常變動的場景，依照**呼叫時的需要帶入不同的物件**作為該function的this。呼叫時立即執行

### this與本文(context)綁定的基本原則
>this的綁定的原則大致可分為四種：
* 預設綁定(Default Binding)
  * 因預設綁定的關係，當function是在普通、未經修飾情況下被呼叫，此時裡面的this會自動指定為**全域物件**
  * 有加上'use strict'宣告為嚴格模式，原本將this綁定至全域物件的行為將轉至undefined
* 隱式綁定(Implicit Binding)
  >即使function被宣告的地方是global scope，只要它成為某個物件參考屬性(reference property)，在那個function被呼叫地當下，該function即被那個物件所包含。
  ```javascript
  function func(){
    console.log(this.a);
  };
  var obj = {
    a : 2,
    foo : func
  };

  obj.foo(); //2
  var func2 = obj.func;
  func2(); // undefined，因為func2為參考對象是window.func
  ```
  >**決定this的關鍵不在於它屬於哪個物件，而是在於function呼叫的時機點**
* 顯示綁定(Explicit Binding)
  >透過.bind()/.apply()/.call()直接綁定this的function
* new 關鍵字綁定
  >傳統物件導向程式語言，建構子是被附接到類別上的特殊方法，再透過new將class實體化時，這個建構子會被呼叫。JavaScript雖然也有new這個關鍵字，運作時也與類別導向的語言行為類似，但由於JavaScript不是一個類別導向程式語言(而是基於原型的物件導向)，所以它的new運作原理並不相同。
  >當一個function前面帶有new被呼叫時，會發生
  * 產生一個新的物件(物件被建構出來)
  * 新建構的物件會被預設的function的this綁定目標，也就是this會指向新建構的物件
  * 除非這個function指定了回傳(return)了它自己的替代物件，否則透過new產生的物件會被自動回傳
  ```javascript
  function foo(a){
    this.a = a;
  };
  var obj = new foo(123);
  console.log(obj.a); // 123
  ```
  ### 結論What's "this" in JavaScript?
  * 這個function的呼叫，是透過new進行的嗎？如果是，那麼this就是被建構出來的物件
  * 這個function是以.call()會.apply()的方式呼叫嗎？或是透過.bind()指定？如果是，那this就是被指定的物件
  * 這個function呼叫時，是否存在某個物件？如果是，那this就是那個物件
  * 如果沒有滿足以上條件，則此function裡的this就一定是全域物件，在嚴格模式下則是undefined
---
## [Day 21 函式的 Combo 技： Cascade](https://ithelp.ithome.com.tw/articles/10193549)
> JavaScript允許沒有return回傳值，沒有return的函式預設回傳undefined。如果把沒有return的undefined改成return this就可以有很多變化

>四則運算範例
```javascript
var calNum = function(num){
  this.num = num;

  this.add = function(newNum){
    this.num += newNum
  };
  this.sub = function(newNum){
    this.num -= newNum
  };
  this.multi = function(newNum){
    this.num *= newNum
  };
  this.division = function(newNum){
    this.num /= newNum
  };
};
```
```javascript
var a = new calNum(100);
console.log(a.num); //100
a.add(100);
console.log(a.num); //200
```
### Cascade
>Cascade也有人稱「Fluent Interface」，將先前範例沒有retrun運算function，以this回傳。這樣可以做出方便閱讀，而且一口氣把想要做的事寫在一起。
```javascript
var calNum = function(num){
  this.num = num;

  this.add = function(newNum){
    this.num += newNum
    return this;
  };
  this.sub = function(newNum){
    this.num -= newNum
    return this;
  };
  this.multi = function(newNum){
    this.num *= newNum
    return this;
  };
  this.division = function(newNum){
    this.num /= newNum
    return this;
  };
};
```
```javascript
var a = calNum(100);
a.add(100).sub(50);
console.log(a); // 150
```
>另外，像JavaScript原本就有sort()，以及ES6之後的filter()、map()以及reduce()也有類似的特性，差別在於回傳的式同一個型別的物件，但內容是運算後的結果。
```javascript
var arr = [1,2,8,0,10,51,23,32,3,7,10,9,18,5];
//把arr陣列中的奇數過濾出來，個別求平方根，由小至大排序
var num = arr.filter(function(a){return a%2 !==0;})
             .map(function(a){return a*a;})
             .sort(function(a,b){return a-b;});
console.log(num); //[1,9,25,49,81,529,2601]
```
---
## [Day 22 深入理解 JavaScript 物件屬性](https://ithelp.ithome.com.tw/articles/10193747)
### Review
>所有基本型別以外的都是物件型別，基本型別如下：
* string
* number
* boolean
* null
* undefined
* symbol(ES6新增)
### JavaScript是物件導向的程式語言嗎?
>Javascript是物件導向程式語言，與其他語言不同的是，它的繼承方法是透過"prototype"來進行實作，大多物件導向程式語言是以類別為基礎(class-based)，但JavaScript沒有class沒有extends，但可以透過「原型」(prototype-based)來建立物件之間的關係

### JavaScript自訂物件
```javascript
var person1 = new Object();
person.name = 'james';

var person2 = {
  name : 'duke'
};
```

### 理解JavaScript建構式
>如果希望JavaScript能像其他物件導向程式語言有類似class的語法，可以借用函式來達成
```javascript
function Person(name ,age ,gender){
  this.name =name;
  this.age=age;
  this.gender=gender;

  this.greeting = function(){
    console.log('hello my name is '+this.name+'.');
  };
};

var james = new Person('james','36', 'female');
james.greeting(); //hello my name is james.
```
>拆解建構流程
>透過new Person()，傳回的物件會有name、age、gender、greeting屬性，而JavaScript會在背景執行Person.call方法，並將james物件傳入，將james作為this的參考物件，然後把這些屬性都新增到james物件當中，但是即使用此方法建立的物件，物件的屬性仍可以透過 . 來進行存取
```javascript
function Person(){
  //略
};
var james = new Person('james',36,'male');
/*
  ==> var james = {};
  ==>Person.call(james,'james',36,'male');
*/

console.log(james.age);// 36
```

### 屬性描述器(Property discriptor)
>ES5開始，可以透過物件模型來存取、刪除、列舉等，這些屬性稱「為屬性描述器」(Property discriptor)，需透過ES5提供的Object.defineProperty()來處理，共可分為六種，除了value之外的值可以不設定外，writable、enumerable及configurable的預設值為true，get、set預設為undefined
* value：屬性的值
* writable：定義屬性的值是否可以被更改，false為唯獨
* enumerable：定義物件是否可以透過fon-in來迭代
* configurable：定義屬性是否可以被刪除、或修改writable、enumerable及configurable設定
* get：物件屬性的getter function
* set：物件屬性的setter function

### Object.defineProperty與Object.getOwnPropertyDescriptor
```javascript
//定義物件屬性
var person = {};
Object.defineProperty(person,'name',{
  value:'james'
});
//檢查物件屬性的狀態描述
Object.getOwnPropertyDescriptor(person,'name');
//{value: "james", writable: false, enumerable: false, configurable: false}

//透過實字方式建立的屬性，預設值會是true
var person2 = {name : 'james'};
Object.getOwnPropertyDescriptor(person2,'name');
//{value: "james", writable: true, enumerable: true, configurable: true}
```
>針對物件一次設定多個屬性
```javascript
Object.defineProperty(person,'name',{
  value:'james',
  writable:false,
  enumerable:false,
  configurable:fasle
});
// 設定configurable 為false後刪除物件屬性將會回傳false，嚴格模式下會出現TypeError錯誤
delete person.name; // return false
```
### 屬性get與set方法
>ES5以前可以透過this.getXXX()與this.setXXX()來作為get與set的存取方法，有了ES5的Object.defineProperty可以更直觀處理。

>此處針對name的屬性定義了get與set的方法，實際上透過另一個屬性_name_來作為name屬性的封裝。需注意定義了get與set方法，表示你要自行控制屬性的存取，就不能再去定義value或writable屬性描述
```javascript
var person = {};
Object.defineProperty(person,'name',{
  get：function(){
    console.log('get');
    return this._name_;
  },
  set：function(name){
    console.log('set');
    this._name_ = name;
  }
});
```
---
## [Day 23 基本型別包裹器 Primitive Wrapper](https://ithelp.ithome.com.tw/articles/10193902)
>JavaScript內建型別可以分為基本型別與物件型別兩大類。而物件型別，又可以再細分幾種建構器(Constructor)：
* String()
* Number()
* Boolean()
* Array()
* Object()
* Function()
* RegExp()
* Date()
* Error()
* Symbol()
>這些建構器都可以透過new關鍵字來產生對應物件，這些Constructor都是JavaScript「內建的函式」

### 基本型別包裹器(Primitive Wrapper)
>在JavaScript中，當我們要試著去存取String、Number與Boolean這三種基本型別的屬性時，它就只會在「那一刻」被轉型為該類別的「物件」，它們的屬性方法由對應的物件所提供，這個對應的物件就是**基本型別包裹器(Primitive Wrapper)**
```javascript
var str = 'hello';
console.log(str.length); //5
```
>背後原理：它會透過對應的物件建構器將'hello'包裝成一個String物件，然後回傳對應的屬性後，即刻消滅恢復成基本型別
```javascript
var str = new String('hello');
str.length;
str = null;
str = 'hello'
```
>分別為物件與基本型別的string設定自訂屬性color，設定時不會出錯，讀取時基本型別的屬性仍是undefined，物件則保留了屬性值
```javascript
var str = 'hello';
typeof str; //string
var strObj = new String('hello');
strObj.color = 'red';
str.color = 'red';

console.log(str.color); //undefined
console.log(strObj.color); //red
```
>包裹器特性
```javascript
var nameStr = new String('james');
typeof nameStr; //String
nameStr instanceof String ; //true
typeof nameStr.valueOf(); //string

var num = new Number(123);
typeof num; //Number
num instanceof Number; //true
typeof num.valueOf(); //number
```
---
## [Day 24 物件與原型鏈](https://ithelp.ithome.com.tw/articles/10194154)
### 原型鏈 Prototype Chain
>透過「原型」繼承可以**讓本來沒有某個屬性的物件去存取其他物件屬性**。也就是說當某個物件要試著去存取「不存在」的屬性時，那麼JavaScript會往它的[[prototype]]原型物件去尋找。
```javascript
//洛克人武器是buster 飛彈
var rockman = {buster:true};
var cutman = {cutter:true};
```
>透過in判斷某個屬性是否可以透過這個物件來存取
```javascript
// 注意，屬性名稱必須是字串
console.log(buster in rockman); //true
console.log(cutter in rockman); //false
```
>以JavaScript來說，可以透過Object.setPrototypeOf()來指定物件原型的關係。物件原型是物件內部屬性，而且無法直接存取(通常會直接被標示為[[prototype]])。原型繼承規則裡，**同一物件無法指定兩種原型物件**
```javascript
//承上例
//指定cutman 為 rockman的 「原型」
Object.setPropertyOf(rockman,cutman);
//原型繼承後，洛克人也可以使用剪刀人的武器了
console.log(cutter in rockman); //true
```
>無法指定兩種原型物件
```javascript
var gutsman = {superArm : true};
Object.setPropertyOf(rockman,gutsman);
console.log(superArm in rockman); //true
console.log(cutter in rockman); //false
```
>原型鏈Prototype Chain
```javascript
var rockman = {buster : true};
var cutman = {cutter : true};
var gutsman = {superArm : true};
Object.setPrototypeOf(rockman,cutman);
Object.setPrototypeOf(cutman,gutsman);

console.log('cutter' in rockman); //true
console.log('superArm' in rockman); //true
```

### 最頂層的原型物件：Object.prototype
>當我們嘗試在某個物件存取一個不存在的物件的屬性時，它會繼續往它的「原型物件」[[prototype]]去尋找，在JavaScript幾乎所有物件(環境宿主物件除外)順著原型鏈找到最頂層級時，都會找到Object.prototype才停止，因為Object.prototype是所有物件的起源。在Object.prototype所提供的所有方法，在JavaScript的所有物件都可以呼叫，例如Object.protorype.hasOwnProperty()、Object.prototype.toStrin()、Object.prototype.valueOf()

### 建構式與原型
```javascript
var Person = function(){};
// 函式也是物件，所以可以透過prototype來擴充每一個透過這個函式所構建的物件
Person.prototype.sayHello = function(){
  console.log("hello");
};
var person1 = Person(); //此處是直接呼叫結果，所以會是undefined
var person2 = new Person();

person2.sayHello();// hello
```
>建構式中建立同名的方法，當物件實體與它的原型同時擁有同樣的屬性或方法，他會**優先存取自己的屬性或方法**，沒有才會順著原型鏈往上找
```javascript
var Person = function(){
  this.sayHello() = function(){
    console.log('hihi');
  };
};
Person.prototype.sayHello = function(){
  console.log('hello');
};
var p = new Person();
p.sayHello(); //hihi
```
>小結
* 物件實體與原型鏈同時擁有相同的屬性或方法，會優先存此自己的屬性或方法
* 如果物件實體找不到某個屬性或方法時，會往原型物件尋找
  * 如果在原型物件或更上層原型物件有發現這個屬性，且屬性是描述的writable為true，則會為這物件實體新增對應的屬性或方法
  * 同上，若該屬性描述writable為false，那麼目標物件就會多出一個「唯讀」的屬性，且事後無法再修改
  * 如果在原型物件或更上層原型物件有發現這個屬性，但這個屬性是一個「設定器」(setter function)，那麼呼叫的永遠是那個呼叫器，目標物件屬性也沒有辦法被重新定義

>判斷屬性是原型繼承而來，或是物件本身所有，範例如上rockman、cutman、gutsman的Object.prototype.setPropertyOf()範例
```javascript
console.log(rockman.hasOwnProperty('buster')); //true
console.log(rockman.hasOwnProperty('superArm')); //false
console.log(rockman.hasOwnProperty('cutter')); //false
```
---
## [Day 25 原型與繼承](https://ithelp.ithome.com.tw/articles/10194356)
