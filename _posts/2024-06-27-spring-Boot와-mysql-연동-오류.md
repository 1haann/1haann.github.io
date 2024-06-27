---
layout: post
title: Spring Boot와 MySQL 연동 오류
date: 2024-06-27 21:29 +0900
description: "Caused by: org.hibernate.HibernateException"
category:   [MySQL]
tags:   [설정]
pin: true
---

> Caused by: org.hibernate.HibernateException: Unable to determine Dialect without JDBC metadata
(please set 'jakarta.persistence.jdbc.url' for common cases or 'hibernate.dialect' when a custom Dialect implementation must be provided)  

Hibernate는 데이터베이스의 JDBC 메타데이터를 통해 사용할 데이터베이스의 Dialect를 결정하는데 이 과정에서 문제 발생  
Spring Boot는 자동으로 Dialect를 인식하지만 경우에 따라 명시적으로 설정해야 할 수도 있다.  

**해결 방법 :** `spring.jpa.properties.hibernate.dialect=org.hibernate.dialect."데이터베이스 종류"Dialect`  
<script src="https://gist.github.com/1haann/21ce574c401c3346d5aa9fe6f83edece.js"></script>  

---

**참고 블로그**  
- [Spring Boot와 MySQL 연동 오류](https://velog.io/@jiwonblue/Spring-Boot%EC%99%80-MySQL-%EC%97%B0%EB%8F%99-%EC%98%A4%EB%A5%98)

