---
layout: post
categories: posts
title: 1. Task, Try and Catch
tags: [try, catch, task]
date-string: DECEMBER 04, 2019
---

# Task


### Task 1

> PID Control

  * 자유로운 line 설계
  * 사고 예방 -> 안정성


### Task 2

> Color Scheduling

  * 라인 위에서 유동적으로 color값 인식


### Task 3

> Signal System

<center>
    <img src="/images/intro/manz-task1.jpg">
</center>


# Try and Catch : Exception

> Separation from real world

  * PID Control : angle of entry
  
    경험적으로 pid 계수 추출
    Line 두께, 센서사이의 거리에 따라 계수 재설정

  * Color Scheduling

    <br>
    PID control -> 컬러센서의 라인 이탈
    <br>
    -> 잘못된 Color 값 지속적으로 인식
    <br>
    -> 하나의 Color 신호에서 여러 번 인식
    
    <br>
    * Solution
        - 같은 Color값 일정 수 이상 누적 시 인터랙션
        - 같은 Color값 중복 인터렉션 예외처리
    
       

> EV3's limit

  * Battery Power
  * Color Sensor RGB Range


#### Next

> link : <a target="_blank" href="https://team4nz.github.io//posts/2019-12-03/Trial-Demo.html"> 02. Trial Demo