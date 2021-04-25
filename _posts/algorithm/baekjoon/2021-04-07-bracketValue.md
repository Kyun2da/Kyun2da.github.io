---
layout: post
title: '[백준 / Python] 2504 괄호의 값'
subtitle:
date: 2021-04-07 14:00:00
author: 'Kyun2da'
header-style: text
tags:
  -
# 0️⃣ 1️⃣ 2️⃣ 3️⃣ 4️⃣ 5️⃣ 6️⃣ 7️⃣ 8️⃣ 9️⃣ 🔟
---

## 1️⃣ 서론

이 문제는 백준 [괄호의 값](https://www.acmicpc.net/problem/2504) 문제에 대한 풀이이며 `파이썬(Python)`으로 해결하였다.

## 2️⃣ 문제 설명

'[', ']', '(', ')' 로 이루어진 문자열이 있다. 괄호의 값을 계산하는 식은 다음과 같다.

- '()' 인 괄호열의 값은 2이다.
- '[]' 인 괄호열의 값은 3이다.
- '(X)' 의 괄호값은 2×값(X) 으로 계산된다.
- '[X]' 의 괄호값은 3×값(X) 으로 계산된다.
- 올바른 괄호열 X와 Y가 결합된 XY의 괄호값은 값(XY)= 값(X)+값(Y) 로 계산된다.

괄호열에 대한 값을 출력하는 문제이다. 단 올바른 괄호 식이 아니면 0을 출력한다.

## 3️⃣ 풀이

이전에 괄호검사는 스택으로 하는 문제를 풀었어서 검사는 쉽게 접근할 수 있었지만 계산을 어떻게 접근해야할지 막막했다.

그러다가 중간 계산 값도 스택에 넣으면 어떨까 하는 생각이 들었고 다행히 이 방법이 잘 맞아서 해결할 수 있었다. 계산 방식은 다음과 같다.

닫힌 괄호가 나오면 그와 일치하는 열린괄호가 나올때까지 스택을 pop한다. 이때 tmp라는 변수로 숫자를 만나면 더해주게 된다. `열린괄호를 만났을 때 tmp가 0이면 그 이전에 숫자가 없었다 즉, 내부에 괄호가 없었다는 뜻이므로 그냥 더해주고 숫자가 있었다면 내부에 괄호가 있었다는 뜻이므로 곱해준다.`

이와 같은 방식으로 계속 스택을 검사하며 문제를 해결할 수 있었다. 코드를 보도록 하자.

## 4️⃣ 코드

```python
import sys

s = input()

stack = []

answer = 0
for x in s:
    if x == ')':
        tmp = 0
        if len(stack) == 0:
            print(0)
            sys.exit(0)
        while len(stack) != 0:
            top = stack.pop()
            if top == '[':
                print(0)
                sys.exit(0)
            elif top == '(':
                if tmp == 0:
                    stack.append(2)
                else:
                    stack.append(tmp * 2)
                break
            else:
                tmp += top
    elif x == ']':
        tmp = 0
        if len(stack) == 0:
            print(0)
            sys.exit(0)
        while len(stack) != 0:
            top = stack.pop()
            if top == '(':
                print(0)
                sys.exit(0)
            elif top == '[':
                if tmp == 0:
                    stack.append(3)
                else:
                    stack.append(tmp * 3)
                break
            else:
                tmp += top
    elif x == '(' or x == '[':
        stack.append(x)
    else:
        print(0)
        sys.exit(0)
    # print(stack)

for i in stack:
    if i == '(' or i == '[':
        print(0)
        sys.exit(0)
    else:
        answer += i

print(answer)
```

## 5️⃣ 마치며

괄호 검사 문제는 흔해서 쉽게 풀 수 있다고 생각했는데 괄호 검사에 계산까지 더해져서 아이디어를 생각해 내는 것이 좀 까다로웠던 문제였던 것 같다.
