---
title: "MySql学习"
date: 2023-05-18 17:03:22
tags: MySql
categories: 数据库
---
1.查看前几条数据-  limit 
2.查看范围 内的数据，包含等于
```java
where age between 20 and 23;
where age >= 20 and age <= 23;
```
3.查看除复旦大学以外
```java
where university NOT IN ("复旦大学");
where university !="复旦大学";
```
4.取出所有年龄值不为空
```java
where age != 'null';
where age IS NOT NULL;
```
5.找到男性且GPA在3.5以上(不包括3.5)
```java
 where gender = 'male' and gpa > '3.5';
```

<!-- more -->

6.找到学校为北大或GPA在3.7以上(不包括3.7)
```java
where university = '北京大学' or gpa > '3.7';
```
7.找到学校为北大、复旦和山大的同学
```java
where university in ('北京大学','复旦大学','山东大学');
```
8.找到gpa在3.5以上(不包括3.5)的山东大学用户 或 gpa在3.8以上(不包括3.8)的复旦大学同学
```java
where (gpa > '3.5' and university = '山东大学') or (gpa > '3.8' and university = '复旦大学');
```
9.查看所有大学中带有北京的
```java
where university like '%北京%';
```
10.复旦大学学生gpa最高值是多少
```java
select Max(gpa) from user_profile where university = '复旦大学';
where university = '复旦大学' order by gpa desc limit 1;
```
11.男性用户有多少人以及他们的平均gpa是多少
```java
// 平均 avg  取值位数 round 求总数 count
select count(gender) as male_num,round(avg(gpa),1) as avg_gpa from user_profile where gender = 'male';
```
12.现在运营想要对每个学校不同性别的用户活跃情况和发帖数量进行分析，请分别计算出每个学校每种性别的用户数、30天内平均活跃天数和平均发帖数量。
```java
select gender,university,count(device_id) as user_num,avg(active_days_within_30) as avg_active_day,avg(question_cnt) as avg_question_cnt from user_profile group by university,gender;
```
12.取出平均发贴数低于5的学校或平均回帖数小于20的学校
聚合函数结果作为筛选条件时，不能用where，而是用having语法，配合重命名即可！！！！
```java
select 
university,
 avg(question_cnt) as avg_question_cnt,
 avg(answer_cnt) as avg_answer_cnt 
 from user_profile 
 group by university having avg_question_cnt < 5 or avg_answer_cnt < 20;
```
13.不同大学的用户平均发帖情况，并按照平均发帖情况进行升序排列
```java
select university,
    avg(question_cnt) as avg_question_cnt
from user_profile
group by university
order by avg_question_cnt  
```
```java
// 倒序的话
select university,
    avg(question_cnt) as avg_question_cnt
from user_profile
group by university
order by avg_question_cnt desc
```
14.联表查询
```java
left JOIN 关联表
select t1.device_id,question_id,result from question_practice_detail t1 left JOIN user_profile t2 on t1.device_id = t2.device_id where university = '浙江大学';
```



