---
title: FreeMarker笔记
author: MuMu
categories: [Java Web]
tags: [FreeMarker]
---

#### 什么是FreeMarker？

FreeMarker是一个模板引擎，一个基于模板生成文本输出的通用工具，使用纯Java编写。

FreeMarker被设计用来生成HTML Web页面，特别是基于MVC模式的应用程序。

虽然FreeMarker具有一些编程的能力，但通常由Java程序准备要显示的数据，由FreeMarker生成页面，通过模板显示准备的数据（如下图）

![](https://cdn.jsdelivr.net/gh/piggy925/BlogAssets@main/uPic/Jw-17.png)

FreeMarker的出现通常是为了替代JSP，通过FreeMarker可以使Java程序员专注于数据的处理，使前端程序员专注于数据的展示。

使用示例：

```java
public class FreemarkerSample1 {
    public static void main(String[] args) throws IOException, TemplateException {
        //1.加载模板
        //创建核心配置对象
        Configuration config = new Configuration(Configuration.VERSION_2_3_28);
        //设置加载的目录
        //FreemarkerSample1类与sample.ftl放在同一个包下，因此后一个参数为空
        config.setClassForTemplateLoading(FreemarkerSample1.class, "");
        //得到模板对象
        Template t = config.getTemplate("sample1.ftl");
        //2.创建数据
        Map<String, Object> data = new HashMap<String, Object>();
        data.put("site", "百度");
        data.put("url", "http://www.baidu.com");
        //3.产生输出
        t.process(data, new OutputStreamWriter(System.out));

    }
}
```

```ftl
<#-- sample.ftl内容 -->
${site}-${url}
```

控制台输出：

![](https://cdn.jsdelivr.net/gh/piggy925/BlogAssets@main/uPic/Jw-18.png)

#### FTL取值

| 表达式                    | 作用                   |
| :------------------------ | :--------------------- |
| ${属性名}                 | 取值                   |
| ${属性名!默认值}          | 属性不存在则使用默认值 |
| ${属性名?string(“.....”)} | 格式化输出             |

```ftl
//时间格式化
${date?string("yyyy-MM-dd")}
//小数点后取两位    
${num?string("0.00")}
```

#### 分支判断

if分支判断：

```ftl
<#if 条件1>
    条件1成立执行代码
<#elseif 条件2>
    条件2成立执行代码
<#elseif 条件3>
    条件3成立执行代码
<#else>
    其他情况下执行代码

<#if 对象.属性??>
	...//属性不为空则执行
</#if>
```

switch分支判断：

```ftl
<#switch value>
    <#case value1>
        ...
        <#break>
    <#case value2>
        ...
        <#break>
    <#case valueN>
        ...
        <#break>
    <#default>
    ...
</#switch>
```

#### 使用list迭代输出

list迭代列表：

```ftl
<#list students as stu>
	${stu_index} //输出索引值，从0开始
	${stu.name} //输出属性值
</#list>
```

list迭代Map：

```ftl
<#list map?keys as key>
	${key} //获取map的key
	${map[key]} //获取map的key所对应的value
</#list>
```

#### FreeMarker整合Servlet

1. 新建JavaWeb项目

2. 添加FreeMarker jar包：[FreeMarker的Maven仓库链接](https://mvnrepository.com/artifact/org.freemarker/freemarker)

```xml
<!-- Maven依赖 -->
<dependency>
    <groupId>org.freemarker</groupId>
    <artifactId>freemarker</artifactId>
    <version>2.3.28</version>
</dependency>
```

3. 在web.xml中配置FreeMarker Servlet

> FreeMarker Servlet的作用：
>
> 当客户端访问地址以.ftl结尾时，FreemarkerServlet会到ftl文件存放地址中查找相应文件并输出

```xml
<servlet>
    <servlet-name>freemarker</servlet-name>
    <servlet-class>freemarker.ext.servlet.FreemarkerServlet</servlet-class>
    <init-param>
        <!-- 设置ftl文件存放地址 -->
        <param-name>TemplatePath</param-name>
        <param-value>/WEB-INF/ftl</param-value>
    </init-param>
</servlet>
<servlet-mapping>
    <servlet-name>freemarker</servlet-name>
    <url-pattern>*.ftl</url-pattern>
</servlet-mapping>
```

4. 定义一个准备数据的servlet

```java’
@WebServlet("/list")
public class ListServlet extends HttpServlet {
    @Override
    protected void doGet(HttpServletRequest req, HttpServletResponse resp) throws ServletException, IOException {
        List list = new ArrayList();
        list.add(...);
        ...

        req.setAttribute("employee_list", list);
        req.getRequestDispatcher("/employee.ftl").forward(req, resp);
    }
}
```

5. 定义接收并展示数据的ftl

```ftl
<#list employee_list as emp>
	<tr>
        <td>${emp_index + 1}</td>
        <td>${emp.empno?string("0")}</td>
        <td>${emp.ename}</td>
        <td>${emp.department}</td>
        <td>${emp.job}</td>
        <td>${emp.salary?string("0.00")}</td>
	</tr>
</#list>
```

6. 浏览器访问页面显示如下

![](https://cdn.jsdelivr.net/gh/piggy925/BlogAssets@main/uPic/Jw-19.png)