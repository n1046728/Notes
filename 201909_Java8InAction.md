
ch2
參數化->類別->匿名類別->lambda

ch3
interface 只定義ㄧ個抽象方法，不論多少默認方法，仍為ㄧ個functional interface

Predicate
-----
@FunctionalInterface
public interface Predicate<T>{
	boolean test(T t);
}


public static <T> List<T> filter(List<T> list, Predicate<T> p) {
List<T> results = new ArrayList<>();
	for(T s: list){
		if(p.test(s)){
			results.add(s);
		}
	}
	return results;
}


Consumer
-----
@FunctionalInterface
public interface Consumer<T>{
	void accept(T t);
}

Function
---
@FunctionalInterface
public interface Function<T, R>{
	R apply(T t);
}


functional interface 不允許拋出受檢異常checked exception
解決方法(測驗3.4下方)
1.定義ㄧ個自己的函數示接口並聲明受檢異常
2.或包在try/catch中

lambda表達示飲用的局部變量必須是final的 p74
local variable 保存在thread上，並且隱式表示他們僅限於其所在thread，如果允許捕捉可改變的局部變量會造成非thread safe
(實體變量變量可以，因為他們保存在heap中，而heap在thead中是共享的)

Apple::getWeight方法引用就是Lambda表達是(Apple a)->a.getWeight()的縮寫
p75
1.指向靜態方法的引用
2.指向任意類型實例方法引用
3.指向現有對象的實例方法引用


3.8 comparator example

5.3 p114
短路求值
布林表達是求值，只須找到ㄧ個表達是為false，就可以將返回false，所以不需計算整個表達式，這就是短路
ex.allMatch、anyMatch、noneMatch、

findFirst、findAny return Optional<T>
-isPresent() 
-ifPresent(Consumer<T> block)
-T get()
-T orElse(T other)

findFirst 會有並行上的限制

5.4 Reducing

imply裝箱成本
int calories = menu.stream()
	.map(Dish::getCalories)
	.reduce(0, Integer::sum);

solve
int calories = menu.stream()
	.mapToInt(Dish::getCalories)
	.sum();

IntStream 裝箱boxed

generate num sequence
IntStream.RangeClosed(1,100)
IntStream.Range(1,100)

Stream<String> stream = Stream.of("Java 8 ", "Lambdas ", "In ", "Action");

int[] numbers = {2, 3, 5, 7, 11, 13};
int sum = Arrays.stream(numbers).sum();

long uniqueWords = 0;
try(Stream<String> lines =
	Files.lines(Paths.get("data.txt"), Charset.defaultCharset())){
	uniqueWords = lines.flatMap(line -> Arrays.stream(line.split(" ")))
	.distinct()
	.count();
}
catch(IOException e){
}


Stream API提供兩個靜態方法來從函數生成流 Stream.iterate、Stream.generate

1.迭代use UnaryOperator<t>

Stream.iterate(0, n -> n + 2)
	.limit(10)
	.forEach(System.out::println);

2.生成 use Supplier<t>
Stream.generate(Math::random)
	.limit(5)
	.forEach(System.out::println);

ch6.

分組
groupingBy
分區：分區是分組的的特殊情況，由ㄧ個謂詞作為分類函數
partitionBy

自定Collector  or use collect(s,a,c)

JMH 性能測試框架


ch7.

parallel內部使用默認的ForkJoinPool，默認的是你處理器執行緒數量

平行化代價：對流做劃分、把每個子流歸納到不同的thread，然後把這些操作結果合併成ㄧ個值

使用parallel 在使用forEach時會有副作用，他會改變多線程共享對象的可變狀態

stream 可分解性
ArrayList 极佳
LinkedList 差
IntStream.range 极佳
Stream.iterate 差
HashSet 好
TreeSet 好

分支/合併框架需要預熱或是說執行幾遍才會被JIT編譯器優化

拆分機制spliterator

自定spliterator


ch8.

匿名類別中，this代表的式類的自身，但lambda他代表的式包含類。其次匿名類可以屏蔽包含類的變量，而Lambda表達式不行
故以下編譯錯誤：
int a = 10;
Runnable r1 = () -> {
	int a = 2;
	System.out.println(a);
};
Runnable r2 = new Runnable(){


以下編譯正常
public void run(){
	int a = 2;
	System.out.println(a);
	}
};


design pattern
策略模式

模板方法

觀察者模式

責任鏈模式

工廠模式

peek操作可以在流的每個元素恢復運行之前插入ㄧ個動作


ch9.
抽象類別 與 抽象介面
ㄧ個類只能繼承ㄧ個抽象類，但是ㄧ個類可以時現多個介面
ㄧ個抽象類別可以通過實體變量保存ㄧ個通用狀態，而介面是不能有實體變量的


public interface A {
	default void hello() {
		System.out.println("Hello from A");
	}
}
public interface B extends A {
	default void hello() {
		System.out.println("Hello from B");
	}
}
public class C implements B, A {
	public static void main(String... args) {
		new C().hello();
	}
}
衝突規則
1.類的方法優先級最高
2.若無法按第一條判斷，那麼子接口的優先級更高
3.若還是無法判斷，繼承多接口的類必須通過顯示覆蓋和調用期望的方法

public class C implements B, A {
	void hello(){
		B.super.hello();
	}
}

菱形繼承
public interface A{
	default void hello(){
		System.out.println("Hello from A");
	}
}
public interface B extends A { }
public interface C extends A { }
public class D implements B, C {
	public static void main(String... args) {
		new D().hello();
	}
}

ch10.

Optional


ch12.

java1.0 java.util.Date 缺點
1.無法表示日期，只能以毫秒的精度表示時間
2.年份的起始是1900年
3.月份的起始從0開始
4.默認時區CST
==>很多方法被deprecate==>java.util.Calendar

java.util.Calendar 缺點
1.月份依舊是從0開始
2.糟糕的是同時存在Calendar、Date兩個類，有的特性只存在某一個類 ex.DateFormat只存在Date類中
3.DateFormat none Thread safe ->若兩個thread 使用同一個formatter可能有無法預期的結果
4.Date和Calendar類都是可變的
==>第三方日期庫Joda-Time
==>java.time (整合Joda time 特性)

ch13.

階乘函數的三種寫法

ch14

1.currying
2.lazy evaluation


