---
title: Tomcat故障与解决方法
author: MuMu
categories: [Java Web]
tags: [Issue, Tomcat]
---

### Q1: Tomcat启动报错 java: 程序包javax.servlet.http不存在

1. Ctrl + Alt + Shift + S进入项目结构设置

![](https://cdn.jsdelivr.net/gh/piggy925/BlogAssets@main/uPic/Jw-11.jpg)

2. 将Tomcat添加到依赖中

![](https://cdn.jsdelivr.net/gh/piggy925/BlogAssets@main/uPic/Jw-12.png)

![](https://cdn.jsdelivr.net/gh/piggy925/BlogAssets@main/uPic/Jw-13.png)

---

### Q2: IDEA中Tomcat日志输出中文乱码

![](https://cdn.jsdelivr.net/gh/piggy925/BlogAssets@main/uPic/Jw-46.png)

1. 找到Tomcat安装目录 -> conf -> logging.properties文件

![](https://cdn.jsdelivr.net/gh/piggy925/BlogAssets@main/uPic/Jw-47.png)

2. 编辑该文件，将所有的UTF-8改为GBA

![](https://cdn.jsdelivr.net/gh/piggy925/BlogAssets@main/uPic/Jw-48.png)

3. 重启Tomcat即可

![](https://cdn.jsdelivr.net/gh/piggy925/BlogAssets@main/uPic/Jw-49.png)