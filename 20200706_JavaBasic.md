## CH14 Java IO

### File(non-stream)
>File類別不是一個標準I/O的類別，在java.io類別他是唯一的non-stream類別，不能讀取也不能改變檔案內容，**主要用於收集檔案或目錄的相關資訊**
* createFile()
>建構File類別(new File(XXX))並不會在實體建立一個真實的檔案，因為new File(xxx)只是在Heap區塊建立一個類別物件的instance，必須搭配creatFile()方法才可以在所指定的檔案系統中建立檔案
* mkdir()
> 建立目錄，若指定的目錄不存在則無法建立(通常因為parent不存在而失敗)，成功：true，失敗：false
* mkdirs()
>建立目錄，若指定的目錄不存在則會先建立所需的parent目錄，之後再建立所要的目錄，成功：true，失敗：false
* isDirectory()
>判斷是檔案還是目錄
* exists()
> 判斷檔案是否存在

### 串流(stream)
>stream是串流的意思，Data stream可翻成資料串流，亦即資料在資料來源端(Data Source)與資料目的端(Data sink)之間流動的概念。
![](imgs/stream.png)

* InputStream與OutputStream
>輸入與輸出byte資料串列(byte stream)
* Reader與Writer
>輸入與輸出character資料串列(characer stream)
* Node Streams
>是可以直接連接到實體資源的Stream物件，所謂實體是指File、Memory與Pipe

### FileInputStream與FileOutputStream
* 分別繼承自InputStream與OutputStream類別，並且是位元導向(byte-oriented)，用來開啟檔案以供讀取檔案內容，若檔案不存在會自動建立新檔
* 主要針對**非文字類**I/O存取，影像、影片、音樂、網路資源等等
```java
byte [] buffer;

try(FileInputStream fis = new FileInputStream("src/photo.jpg") 
    FileOutputStream fos = new FileOutputStream("src/photo_copy.jpg")){
    
    buffer = new byte[1];
    while(fis.read(buffer) != -1){
        fos.write(buffer);
    }

}catch(IOException e){}
```
* 抓取網路圖片
  * URL定義URL物件
  * URLConnection定義URL連線物件
> new Url("http://XXXX") ->openConnection() ->getInputStream()

### FileReader與FileWtiter
* 分別是InputStreamReader與OutputStreamWriter的子類別
* 主要針對**文字類**I/O進行存取
```java
String data ="hello world";
System.out.println("將字串： "+data+"寫到檔案");
System.out.println("資料長度："+data.length()+"bytes.");
try(FileWriter fw = new FileWriter("C:/test.txt");){
    fw.write(data);
}catch(IOException e){
	e.printStackTrace();
}
```
```java
char[] buffer = new char[1];
try(FileReader fr = new FileReader("D:/test.txt");){
    while(fr.read(buffer) != -1){
        //一個英文字與中文字都是一個char
        System.out.println(new String(buffer));
    }
    System.out.println();
}catch(IOException e){
    e.printStackTrace();
}
```
### Processing Streams
>是在程式中站存或執行資料處理時的Stream物件

### I/O Chain
>為追求效能，在實作java I/O程式時，通常不會只用單一的I/O來存取Source與Sink端中的資料
![](imgs/java_iochain.png)
### BufferReader與BufferWriter
> 利用資源緩衝區(Buffer)可大量降低檔案操作的次數，增加執行效率
* BufferReader與BufferWriter
  * 字元導向，讀取資料時可以不用逐字讀取，可利用readLine()做逐行讀取，增加讀取效率
* BufferInputStream與BufferOutputStream
  * 位元導向
![](imgs/java_iochain02.png)
```java
try(FileReader fr = new FileReader("D:/test.txt");
    BufferReader br = new BufferReader();){
    
    String data;
    while((data = br.readLine() != null)){
        System.out.println(data);
    }
}catch(IOException e){
    e.printStackTrace();
}

```
>BufferedWriter每次write()是先進入buffer暫存區，暫存區滿了才會stream進行存取
```java
String [] res = {"hello","world"};
try(FileWriter fw = new FileWriter("D:/test2.txt");
    BufferedWriter bw = new BufferedWriter(fw);){
    //BufferedWriter bw = new BufferedWriter(fw,8*1024); //buffer = 8k
    for(String data : res){
        bw.write(data);
        bw.newLine();
    }
    System.out.println("file is completed");
}catch(IOException e){
    e.printStackTrace();
}
```

### Console主控台I/O
* System.in
  > 標準輸入裝置是一個InputStream物件，但System.in不可單獨使用，必須內含在某個InputStream物件中，預設資料來源為鍵盤
* System.out
  >標準輸出裝置是一個可以單獨使用的PrintStream物件，預設輸出裝置為螢幕
* System.err
  >標準顯示錯誤裝置使一個可以單獨使用的PrintStream物件，預設輸出裝置為螢幕
```java
try(FileOutputStream fos = new FileOutputStream("D:/test3.txt");
    BufferedOutputStream bos = new BufferedOutputStream(fos);
    PrintStream out = new PrintStream(bos);){

    //設定輸出為檔案
    System.setOut(out);
    System.out.println("hello");
    System.out.println("world");
}catch(IOException e){e.printStackTrace();}

```
### 物件序列化
>物件序列化就是將物件轉換成一種連續bytes資料，用以存放(存檔)或在網路環境中的遠端傳遞(RMI)，以便日後能還原序列化的狀態。在java中只要implements Serilizable即可

```java
public class Employee implements Serilizable{
    private String name;
    private String salary;
}
```
```java
try(FileOutputStream fos = new FileOutputStream("D:/test.ser");
    ObjectOutputStream oos = new ObjectOutputStream(oos);){

    Employee e = new Employee("james","100000");
    oos.writeObject(e);
    System.out.println("success");
}catch(IOException e){
    System.out.println("failure");
}
```
```java
try(FileInputStream fis = new FileInputStream("D:/test.ser");
    ObjectInputStream ois = new ObjectInputStream(fis);){
    
    Employee e = (Employee) ois.readObject();
    if(e != null)
        System.out.println(e);
    else
        System.out.println(null);
}catch(IOException e){
    e.printStackTrace();
}

```
### LAB01
> 利用FileReader/FileWriter撰寫一個Copy.java, 使其可以將 src/res/NewFile.txt的檔案內容複製到 src/res/Backup.txt內
```java
try(FileReader fr = new FileReader("D:/test.txt");
    BufferedReader br = new BufferedReader(fr,8*1024); 
    FileWriter fw = new FileWriter("D:/copy.txt");
    BufferedWriter bw = new BufferedWriter(fw , 8*1024);){
    
    String line;
    while(( line= br.readLine()) != null){
        bw.write(line);
        bw.newLine();
}			
}catch(IOException e){
    e.printStackTrace();
}finally{
    System.out.println("program is done");
}
```
### LAB02
>利用BufferedInputStream與BufferedOutoutStream來取得網路資源圖片並存檔成android.png  
API:
http://docs.oracle.com/javase/7/docs/api/java/io/BufferedInputStream.html
http://docs.oracle.com/javase/7/docs/api/java/io/BufferedOutputStream.html
網路圖片資源:
http://developer.android.com/images/home/android-jellybean.png

```java
String path = "https://s.yimg.com/ny/api/res/1.2/02GJwNY0CrsN_1tEGszWDw--~A/YXBwaWQ9aGlnaGxhbmRlcjtzbT0xO3c9ODAw/https://media.zenfs.com/zh-tw/ftvn.com.tw/30bc89774d4b85a8554bd1d1769bce52";
		URL url = new URL(path);
		InputStream stream = url.openStream();
		
		try(BufferedInputStream bis = new BufferedInputStream(stream);
			FileOutputStream fos = new FileOutputStream("D:/nadal.jpg");
			BufferedOutputStream bos = new BufferedOutputStream(fos)){
			byte[] data = new byte[1];
			while(bis.read(data) != -1){
				bos.write(data);
			}
		}catch(IOException e){
			e.printStackTrace();
		}finally{
			System.out.println("program is done");
		}

```

---
## CH01 Java Basic
### Java 程式結構
* constructor屬物件成員，不可加上static
* 區域變數不可加上static，生命週期僅限於方法或建構子區塊
* void的方法不用return回傳值，若要使用可以return;
* instance variable 會給初始值，區域變數則無 
```java
public class Puppy{
    static String dogType = "Husky"; //類別變數 class variable
    private String dogName = "lacky"; //物件變數 (non-static member/instance member)
    private String dogColor = "yellow";
    void skill(){ //Object method
        String skill1 = "bark"; //local variable
        String skill2 = "bite"; 
    }
    static void move(){ //static method

    }
    Puppy(){}// constructor
    public static void main(String []args){ //程式進入點

    }
}
```
### 註解
* 單行：//
* 多行：/**/
* 文件註解：/** */
  > javadoc -verbose -private -d ./docs Dog.java
* Annotation：一種metadata註解，用來描述資料的資料

### 存取修飾元
| 存取修飾元 | 權限                                                      |
| ---------- | --------------------------------------------------------- |
| private    | 同一個class                                               |
| default    | 同一package的class才可存取                                |
| protected  | 同一package的class才可存取，不同package需透過繼承才可存取 |
| public     | 皆可存取                                                  |

### 資料型別
#### 變數儲存方式
* Global：存放被宣告為static的類別變數
* Stack：存放primitive type 與reference type的值
* Heap：存放reference type 的實體
![](imgs/java_memory.png)

#### Primitive type
#### Reference type

### 陣列
* 陣列宣告
  ```java
  int [] arr1 = new int[]{1,2,3,4};
  int [] arr2 = {1,2,3,4,5};
  ```
* 陣列就是物件
  ```java
  Object o = new int[10]; //多型宣告
  ```
* 字串就是char[]
  ```java
  String str = new String(char[] c);
  ```
* 陣列長度length
* 字串長度length()

### 字串immutable
>String
```java
String s1 = "java";
s1 = s1.replace("j","l");
System.out.println(s); //lava

String s2 = "java";
s2.replace("j","l");
System.out.println(s); //java
```
>StringBuffer
* 指的是一連串的可變動Unicode字元
* append()、insert()
```java
StringBuffer bf = new StringBuffer("Hello");
bf.append(" world");
System.out.println(bf.toString()); //Hello world
```

## 流程控制
### switch-case
* switch(x)：x必須是byte、char、short或int，java7支援String
* 值域小於int的會自動做隱式轉換成int再交由switch-case執行，若是long或double則須用**強制轉換語法轉換**成int
* only one比對參數
* default可以單獨存在於switch-case中，僅能有一個default
```java
char x = 'A';
switch(x) {
    case 65:
    System.out.print("A");
    break;    
    case 66:
    System.out.print("B");
}
```
```java
char x = 'A';
char valueA ='A'; //comile error：case must be constant expression
// final char valueA = 'A'; //ok
switch(x) {
    case valueA:
    System.out.print("A");
    break;    
    case 'B':
    System.out.print("B");
}

```
* ASCII table
  * 97 : a
  * 65 : A
  * 0 :null 

### for-loop
* 無窮迴圈表示法：for(;;)
* 空實作：for(;;);

## CH02 物件導向
### 繼承(Inheritance)
### 封裝(Encapsulation)
### 多型(Polymorphism)
### 覆寫(Overriding)
  * 遮蔽：方法有覆寫機制，屬性也有，屬性的覆寫機制稱為遮蔽。單純的將父類別的覆蓋，仍可以透過super取得
### 多載(Overloading)
### 介面
### 抽象類別
### 內部類別
### 列舉

### Regular Expression

```java
//first
Pattern p1 = Pattern.compile("java.");
Matcher m1 = p1.matcher("java8");
boolean result1 = m1.matches();

//second
boolean result2 = Pattern.compile("java.").matcher("java8").matches();

//third
boolean result3 = Pattern.matches("java.","java8");

```
### LAB
* 信用卡格式表示式
* 身分證格式表示式
* 電子郵件表示式

## NIO
```java
public class Main {
	public static void main (String [] args) throws IOException {	
		String path = "https://s.yimg.com/ny/api/res/1.2/02GJwNY0CrsN_1tEGszWDw--~A/YXBwaWQ9aGlnaGxhbmRlcjtzbT0xO3c9ODAw/https://media.zenfs.com/zh-tw/ftvn.com.tw/30bc89774d4b85a8554bd1d1769bce52";
		URL url = new URL(path);
		InputStream stream = url.openStream();
		Path dest = Paths.get("D:/nadal2.jpg");
		try(BufferedInputStream bis = new BufferedInputStream(stream)){
			Files.copy(bis, dest, StandardCopyOption.REPLACE_EXISTING);
		}catch(IOException e){
			e.printStackTrace();
		}finally{
			System.out.println("program is done");
		}
	}
}

```
