---
layout: post
title: '[백준 / Python] 1918 후위 표기식'
subtitle: 스택
date: 2021-05-13 15:00:00
author: 'Kyun2da'
header-img: 'img/post-bg-universe.jpg'
tags:
  - 알고리즘
  - 스택
# 0️⃣ 1️⃣ 2️⃣ 3️⃣ 4️⃣ 5️⃣ 6️⃣ 7️⃣ 8️⃣ 9️⃣ 🔟
---

## 1️⃣ 서론

이 문제는 백준 [1918 후위 표기식](https://www.acmicpc.net/problem/1918) 문제에 대한 풀이이며 `파이썬(Python)`으로 해결하였다.

## 2️⃣ 문제 설명

이 문제는 중위 표기법으로 되어 있는 식을 후위 표기법으로 바꾸는 문제이다.

## 3️⃣ 풀이

중위 표기법을 후위 표기법으로 바꾸는 과정은 다음과 같다.

1. 피연산자가 들어오면 바로 출력한다.
2. 연산자가 들어오면 자기보다 우선순위가 높거나 같은 것들을 빼고 자신을 스택에 담는다.
3. 여는 괄호를 만나면 무조건 스택에 담는다.
4. 닫는 괄호를 만나면 여는 괄호를 만날때 까지 스택에서 출력한다.

이를 코드로 표현하면 아래와 같다.

## 4️⃣ 코드

```python
expression = input()

stack = []
ans = ""
for s in expression:
    if s == '+' or s == '-':
        while stack and stack[-1] != '(':
            ans += stack.pop()
        stack.append(s)
    elif s == '*' or s == '/':
        while stack and (stack[-1] == '*' or stack[-1] == '/'):
            ans += stack.pop()
        stack.append(s)
    elif s == '(':
        stack.append(s)
    elif s == ')':
        while stack and stack[-1] != '(':
            ans += stack.pop()
        stack.pop()
    else:
        ans += s

while stack:
    ans += stack.pop()

print(ans)
```

## 5️⃣ 마치며

중위 표기법을 후위 표기법으로 바꾸는 방법을 알아보았다. 미리 바꾸는 방법을 숙지하고 있었다면 쉬운 문제가 될 수 있지만, 그렇지 않다면 바꾸는 방법을 생각해야해서 어려웠던 문제였던 것 같다.
