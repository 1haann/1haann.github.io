---
layout: post
title: MySQLWorkbench new Connection 오류
date: 2024-06-27 21:41 +0900
description: "Access denied for user '유저아이디'@'localhost' (using password: YES) 에러"
category:   [MySQL]
tags:   [이슈]
pin: true
---

> MySQL Workbench에서 새로운 커넥션을 만드는 과정 중 에러가 발생했다.  
Access denied for user '유저아이디'@'localhost' (using password: yes)  

![Failed to Connect to MySQL](../assets/img/myPostImages/connect_fail.png)  

**결론 : 구글링 하면서 이것저것 다 해봤는데 권한 문제였다.**  
<br>

**root 사용자로 접속 :** `mysql -u root -p`
![mysql 로그인](../assets/img/myPostImages/sql_login.png)  
<br>

**유저아이디 권한 확인 :** `SELECT host, user FROM mysql.user WHERE user = '유저아이디';`
![권한 확인](../assets/img/myPostImages/host_qualification.png)  
<br>

**권한 부여 :** `GRANT ALL PRIVILEGES ON DB명.* TO '유저아이디'@'localhost' IDENTIFIED BY '비밀번호';`  
![권한 부여](../assets/img/myPostImages/give_qualification.png)
![Flush](../assets/img/myPostImages/flush.png)  
**MySql 8.0 이후부터는 계정 생성과 권한 부여를 한 번에 할 수 없다고 한다. 위의 생성, 권한 과정을 분리해야 함**  
<br>

**root 계정 접속**
![Workbench 메인](../assets/img/myPostImages/workbench_main.png)  
<br>

**Users and Privileges 탭으로 이동 후 Add account**
![계정 생성](../assets/img/myPostImages/add_account.png)  
<br>

**유저아이디와 비밀번호 입력 후 Apply**
<script src="https://gist.github.com/1haann/36e6c41429fa58d1973064bd8b2fab00.js"></script>

![아이디,비밀번호 입력](../assets/img/myPostImages/add_account_input.png)  
<br>

**생성 결과**
![계정 생성 결과](../assets/img/myPostImages/add_account_result.png)  
<br>

**메인 화면 Setup New Connection**
![New Connection](../assets/img/myPostImages/new_connection.png)  
<br>

**성공 화면**
![성공 화면](../assets/img/myPostImages/success.png)  
<br>

---

**참고 블로그**  

- [손지민 블로그 - ERROR 1064(42000)](https://velog.io/@s0nnyday/posts)
- [오늘의 개발 블로그 - Access denied for user '유저아이디'](https://oneul-losnue.tistory.com/108)
- [myeonji 블로그 - Access denied for user '유저아이디'](https://velog.io/@rladuswl/MySQL-%EC%97%B0%EB%8F%99-%EC%97%90%EB%9F%AC)