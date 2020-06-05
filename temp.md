# Ch1 簡介Web應用程式

## URI
>* URN
>* URL：以文字方式說明網路上資源如何取得

## URI Encoding
>* 保留字元：:、&、=、@、%等
>* 跳脫字元：%之後以16進位數值表示方式該字元的八個位元數值
>EX.「:」為0011010，以16進位表示為3A
>* 中文字元：URI-Encoding不限制使用utf-8，ms950也可，後端須了解如何decoding
>* java相關：java.net.URLEncoder.encode()、URLDecoder.decode()
---
## HTTP
### 特性：
  >* Request/Response
    >1. Http/1.1：同一連線多次請求，依序返回
    >2. Http/2：支援Server Push，允許接到請求，主動推送
  >* stateless 協定：response後不會記得瀏覽器狀態
---
## HTTP Request

### GET
* Request parameter：path?file=servlet&user=caterpillar
* Rquest parameter長度有限，不適合資料量大的
* Request Parameter會在網址列看到

### POST
* Request parameter 在Message Body中
* 適合大資料量
* 請求參數不會在網址列，但非加密連線參數仍會有被看到，機密資料務必在加密連線重送

### 安全與等冪
>* 安全方法是指在實作應用程式時，必須避免有使用者非預期中的結果
>* 等冪，單一請求產生的副作用，與同樣請求進行多次的副作用必須是相同的
>* POST不具等冪，GET HEAD PUT DELETE是等冪方法
---
## [REST (Representational State Transfer)](https://zh.wikipedia.org/wiki/%E8%A1%A8%E7%8E%B0%E5%B1%82%E7%8A%B6%E6%80%81%E8%BD%AC%E6%8D%A2)
>* Stateless，基於HTTP/1.0
>* 符合REST架構的系統稱為RESTful
>* 可搭配Javascript 發出GET、POST、PUT、DELETE請求
---
## Web 安全觀念
* [OWASP Open Application Security Project](https://owasp.org/www-project-top-ten/)：針對Web應用程式最重大的10個弱點進行排行，3年一次
* [CWE Common Weakness Enumeration](https://cwe.mitre.org/data/)弱點清單
* [CVE Common Vunlnerabilities and Exposure](https://cve.mitre.org/cve/)：
  >CVE會就特定軟體發生的安全問題給予CVE-YYYY-NNNN形式的編號，方便查詢、通報、交流等。
---
Web 容器Container
>對Java程式而言，JVM是其作業系統，容器就是一個用Java寫的程式，運行於JVM上，容器的概念它布僅持有物件，還負責物件的生命週期與相關服務的連結。
