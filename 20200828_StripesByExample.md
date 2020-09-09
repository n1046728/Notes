# Stripes by Example
## CH03
### ActionBean
>Server side code
### Stripes tag
>The purpose of the tags in Stripes is to interact with your ActionBean.
	
### ActionBeanContext 
>provides access to all of the HTTP request/response objects.
		For example, the HttpServletRequest, HttpServletReponse, and also ValidationError
		and Message objects that are used to pass messages back to the user from the server.
### BaseActionBean
> 1.Refactoring to Remove Duplication  
	2.This not only helps follow the DRY principle of software development (Don’t Repeat Yourself ), but also provides a central place to add additional common feature methods—for example, a
			isUserLoggedIn() method, a getDatabaseFactory() method, or even logging methods
## CH04 Mapping URLs to Method
### @UrlBinding
>is a class-level annotation that defines the base URL that is used to access an ActionBean. As
### @HandlesEvent
>annotation is a method-level annotation that is used to define the method to be executed, 
depending on the last part of the URL navigated to by the user.
### @DefaultHandler
### 問題solve
> 1. jstl 無法正常使用org.apache.jasper.JasperException:   
		The absolute uri: http://java.sun.com/jsp/jstl/core cannot be resolved in either web.xml or the jar files deployed with this application  
	2. solve
		>copy D:\apache-tomcat-8.0.33\webapps\examples\WEB-INF\lib  to eclpse project WEB-INF/lib
			taglibs-standard-impl-1.2.5.jar
			taglibs-standard-spec-1.2.5.jar
 
## CH05 JSP
1. Using ${topic} vs. <c:out value="${topic}" /> would also work. I personally
		do not use c:out, but you may see it elsewhere.
2. \<stripes:param>  
			https://jaxenter.com/tutorial-stripes-a-lean-mean-java-web-framework-104577.html
3. Stripes Form Tags
> Stripes form tags is that each tag must have a
			backing ActionBean property. For example, for a <stripes:text name="bookTitle" />
			tag in your ActionBean, you must have private String bookTitle in your Java
			code—along with getter and setter methods.
## CH06 Forms
1. DTO
>This idea of using objects to store and transfer data between application tiers is a
design pattern called a data transfer object, or a transfer object, or a value object

## CH07 Working with Data
### 
問題solve
1. ch07 application_menu.jsp一直跳不出來，出現錯訊
	The value supplied for the 'beanclass' attribute does not represent a valid ActionBean. The value supplied was 'org.stripesbook.chapter08.Page2ActionBean'.  
solve：Page2ActionBean.java 忘了加入extends BaseAction

2. 待解
			\<li>
				<stripes:link href="/WEB-INF${pageContext.request.contextPath}/jsp/chapter08/page3.jsp">
					Direct jsp link
				</stripes:link>
			</li>	
      
## CH08 Interaction Between with ActionBeans
## CH09 validation
### @Validate
### @ValidateNestedProperties
### @DontValidate
### 問題
1. ch09 advanced 在@validatenestedProperties jsp驗證正確卻無法跳頁

## CH10 Resolutions
### ForwardResolution
>is used to specify the JSP that will be run
### RedirectResolution
>is used to perform an HTTP redirect
### StreamingResolution
>is used to stream data back to the client (such as text or file data)
### ErrorResolution
>takes an error number (e.g., 404) and a message to send back to the client.

### 問題
1. static property 的getter & setter不能是static method  
2. ErrorResolution not work 待解

## CH11 other annotation
### @SessionScope: Used to store ActionBeans in session
### @Before and @After: Useful for performing preprocessing or postprocessing operations in your code
### @SpringBean: Provides a simple facility to integrate with the Spring framework

## CH13 Inerceptors
### Interceptors
>Stripes provides a facility to add hooks at various stages of your application.
Interceptors are classes that implement Stripes’ Interceptor interface and contain an intercept() method
great way to do things like log requests or build security into an application.
Interceptors use the same LifecycleStage enums

### CH14
#### 問題
1. fileupload 檔名出現亂碼
### CH15

	
