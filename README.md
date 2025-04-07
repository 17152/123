Introduction to pigx（pigx 简介）
The pigX framework is a microservice development framework based on Spring Cloud. It integrates excellent frameworks such as Spring Boot, MyBatis, and MyBatis-Plus, and provides a complete microservice solution. PigX is committed to simplifying the microservice development process, improving development efficiency, and provides a wealth of functional modules, such as authentication and authorization, monitoring, and log management.

Vulnerability description（漏洞描述）
As mentioned in the previous introduction, the pigX framework is a microservice development framework based on Spring Cloud, but the pigX framework is in Spring Cloud. After enabling Actuator in the project, by default, we can access any interface without restriction. Some of these interfaces expose very sensitive information, such as: /env, /configprops, /threaddump and other interfaces, which directly display all information.

Loophole principle（漏洞原理）
When visiting a website, the brute force path method is found to exist /admin/actuator. At this time, check whether there is a heapdump file, download and decompress it, and search globally to find the key leak. After getting the file address, visit and download, and use tools to crawl the content after downloading. Found leaked ak\sk

Case reproduction（案例复现）
As shown, this is a test site
![image](https://github.com/user-attachments/assets/a1aee895-4322-4a47-9c34-b664840f76a5)

By brute-forcing the website, we found that /admin/actuator exists.
http://ip:port/admin/actuator

A large number of endpoints were found on this page
![image](https://github.com/user-attachments/assets/1e8c2f4a-3287-4d4d-8071-a4899d960df7)


Then connect heapdump to http://ip:port/admin/actuator, you can download the heapdump file and decrypt it to get the aksk of the cloud storage bucket
![image](https://github.com/user-attachments/assets/5056d8ef-cb3b-44f7-b5d1-2e2673327ee9)

You can take over the bucket
![image](https://github.com/user-attachments/assets/d0dbc7d5-64f8-4f1b-a4e8-0b9d7110b021)


Tool link: https://github.com/whwlsfb/JDumpSpider


The affected version（受影响的版本）
PigX rapid development framework  v 4.0
PigX rapid development framework  v 3.0.0
PigX rapid development framework  v 4.5


