# 조건문이 필요한 이유

특정 상황에 따라 프로그램은 다르게 처리해야 하는 경우가 많다.

예를 들어, '취약' 상태의 캐릭터는 피해량의 20%를 추가로 받는다고 가정하자.  
그러면 '취약' 상태를 **판단해야 하는 경우가 발생**하고, 그러한 상태인지 아닌지를 구분지어 처리해야 한다.

다른 예를 들어, '온라인' 상태의 사용자는 친구 목록에 온라인 탭에 출력해주어야 한다.  
이 또한 '온라인' 상태를 **판단해야 하는 경우가 발생**하고, 그러한 상태인지 아닌지를 구분지어 처리해야 한다.

이처럼 프로그램은 각각의 상황이나 조건에 맞는 처리가 필요한 순간이 반드시 발생한다.

## 표현식(Expression)

표현식은 *평가(evaulate)되며, 값을 반환한다.  
반환된 값은, 표현식에 자리에 남는 것이 핵심이다.  

> **평가(Evaulate)**  
    평가의 간단한 이해는 "결과를 도출하는 과정 또는 그러한 행위"를 의미한다.   

이때 반환의 경우에는 `void`반환을 포함한다.

다음은 대표적인 표현식의 예이다.
* 숫자 그 자체: `10`
* 산술 연산: `5 + 8`
* 변수 호출: `damage`
* 비교(관계): `10 > 5`

그리고 일부 표현식은 단독으로 사용할 수 없다.
```cs
3 + 4;      // Compile Error
age > 19;   // Compile Error
```
## 구문(Statement)
구문은 한 줄 이상의 코드로 **실행**되는 집합을 의미한다.  
즉, 구문은 하나의 **동작을 수행**한다.

또한 구문 내부에는 한 개 이상의 표현식이 포함될 수 있다.

쉽게 말해, 컴퓨터에게 어떤 행동을 지시하고 명령하는 완성된 문장이다.  
보통 세미콜론(`;`)을 붙여 명령이 끝나는 지점을 표시한다.  
또는 중괄호(`{}`)를 사용하여 명령의 시작과 끝을 표시한다.

다음은 대표적인 구문의 예이다.
* 선언 및 대입 구문: `float damage = 12.54f;`  
    (메모리에 공간을 만들고 5를 넣으라는 명령)
* 출력 구문: `Debug.Log($"Damage: {damage}");`  
    (디버깅 창에 로그를 출력하라는 명령)

## Condition (조건)

프로그래밍에서 조건이란, '참'이나 '거짓'을 판별할 수 있는 식이나 구문을 말한다.

이는, 식이나 문장이 **평가**되어 도출된 결과는 반드시 `bool`타입이어야 한다.  
즉, `true` 또는 `false`여야 한다.


C/C++는 `0`을 `false`로, `0`이 아닌 모든 값을 `true`로 취급한다.  
C#은 `bool` 타입이 따로 존재하기 때문에, `true`와 `false`를 숫자와 대응시켜 나타내지도 않고 허용하지도 않는다.

# `if` Statement

`if`문은 '조건'을 만족하면, 중괄호(`{}`) 내부의 코드를 수행한다.

문법적 구조는 다음과 같다.
```cs
if (condition)
{
    // true condition codes...
}
```

## `if`/`else` Statment

`if` 조건문은 항상 조건을 만족하는 경우만을 처리하지는 않는다.  
`if`문의 '조건'을 만족하지 않으면, `else`문의 중괄호(`{}`) 내부의 코드를 수행한다.

문법적 구조는 다음과 같다.
```cs
if (condition)
{
    // true condition codes...
}
else
{
    // false condition codes...
}
```

`else`는 항상 `if` 구문을 우선적으로 필요로 하며, 단독으로 사용할 수 없다.  
다음과 같이 `else`를 단독으로 사용하면 컴파일 에러가 발생한다.
```cs
else  // Not found Condition - if statement
{
    // what the codes...
}
```
에러가 발생하는 이유는 `if`구문에서 선제적으로 '조건'을 판단해야 실행될 수 있는 구문이므로, 조건에 대한 평가 없이 단독으로 사용할 수 없기 때문이다.

## `else if` Statment

`if` 또는 `else` 구문 내부에 또 다른 분기를 만들 수도 있다.
즉, 다음과 같이 중첩된 구조를 가질 수 있다.
```cs
if (condition1)
{
    // true condition1 codes...
}
else
{
    if (condition2)
    {
        // false condition1...
        // and
        // true condition2 codes...
    }
    else
    {
        // false condition1...
        // and
        // false condition2 codes...
    }
}
```

하지만 이러한 중첩 구조가 반복되면 들여쓰기로 인해 가독성이 현저히 떨어진다.  
중첩된 `if`/`else`를 보완하기 위해서 `else if` 구문이 존재한다.

`else if`는 앞선 `if`의 조건이 거짓일 때 실행되는 `else`의 특성과, 조건을 판단하는 `if`의 특성을 모두 가진 구문이다.

즉, 앞선 `if`의 조건이 거짓이며 또 다른 조건을 판단해야 할 때 사용된다.

문법적 구조와 논리적 흐름은 다음과 같다.  
또한 이전의 코드는 다음의 코드와 완벽하게 일치한다.
```cs
if (condition1)
{
    // true condition1 codes...
}
else if (condition2)
{
    // false condition1...
    // and
    // true condition2 codes...
}
else
{
    // false condition1...
    // and
    // false condition2 codes...
}
```

또한 `if` 구문을 시작으로, `else if`가 반복되며 사용될 수 있다.  
또한 `else if`와 `else`는 선택적으로 사용될 수 있다.

# **Coding Stadard : `{}`를 반드시 사용**

앞서 보인 `if`, `else if`, `else` 모두 중괄호(`{}`)를 생략할 수 있다.  
중괄호의 생략은 `if`, `else if`, `else`의 중괄호 내부 코드가 단 한 줄로 표현이 가능한 경우 가능하다.  

예를 들어 다음과 같다.
```cs
int num = 10;

if (num < 10)
    num = 1;
else if (num > 10)
    num = 100;
else
    num = 1000;
```

하지만 이러한 문법적 허용이 반드시 좋은 것만은 아니다.

코드는 항상 수정이 빈번하게 일어나고, 그 과정에서 실수 발생의 확률이 현저히 증가한다.  
따라서 위 예제에서 출력문을 추가해야 할 경우 다음과 같이 생략된 중괄호로 인해 실수가 발생한다.

```cs
int num = 10;

if (num < 10)
    num = 1;
    Debug.Log(num + 1);
else if (num > 10)
    num = 100;
    Debug.Log(num + 2);
else
    num = 1000;
    Debug.Log(num + 3);
```

`num = 1`까지는 `if`문의 범위로 인정되지만, `Debug.Log(num + 1);`는 독립적인 코드로 인식한다.

그렇다면, 이후에 위치한 `else if`는 앞선 `if`에 찾을 수 없다는 에러가 발생된다.

즉, 위 코드는 다음과 같은 코드로 인식된다.
```cs
int num = 10;

if (num < 10)
    num = 1;

Debug.Log(num + 1);

else if (num > 10)
    num = 100;
    Debug.Log(num + 2);
else
    num = 1000;
    Debug.Log(num + 3);
```

따라서 컴파일러 입장에서는 `else if`와 `else`가 `if` 없이 사용되고 있다 판단할 수밖에 없기 때문에 필연적으로 에러가 발생하게 된다.

그러므로 다음과 같이 중괄호를 사용하여 실수를 방지할 수 있다.

```cs
int num = 10;

if (num < 10)
{
    num = 1;
    Debug.Log(num + 1);
}
else if (num > 10)
{
    num = 100;
    Debug.Log(num + 2);
}
else
{
    num = 1000;
    Debug.Log(num + 3);
}
```

이렇듯 처음부터 중괄호를 사용하여 `if`, `else if`, `else`문의 범위를 명확하게 구분해주는 습관은 매우 중요하게 작용한다.
