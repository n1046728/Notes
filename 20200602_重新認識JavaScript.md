# 重新認識 JavaScript筆記
## Content  
>[Day 02 JavaScript 簡介](#day-02-javascript簡介)  
>[Day 03 變數與資料型別](#day-03-變數與資料型別)  
>[Day 04 物件、陣列及型別判斷](#day-04-物件陣列及型別判斷)  
>[Day 05 JavaScript_是「傳值」或「傳址」？](#day-05-javascript-是傳值或傳址)  
>[Day 06 運算式與運算子](#Day&nbsp;06&nbsp;運算式與運算子)  
>[Day 07 「比較」與自動轉型的規則](#Day-07-比較與自動轉型的規則)  
>[Day 08 Boolean 的真假判斷](#Day-08-Boolean-的真假判斷)  
>[Day 09 流程判斷與迴圈](#Day-09-流程判斷與迴圈)  
>[Day 10 函式 Functions 的基本概念](Day-10-函式-Functions-的基本概念)
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
  >javascript中沒有所謂全域變數，所以我們說的全域變數其實式全域物件(或叫頂層物件)，全域物件指的就是window，在node環境下叫做global
* 變數的有效範圍scope的最小切分為function(ES6中的let與const除外)
* 寫在函式內但沒有var的變數會變成全域變數
* 全域變數指的是全域物件(頂層物件)的屬性
  ```javascript
  var a = 10;
  console.log(window.a);// 10
  ```
