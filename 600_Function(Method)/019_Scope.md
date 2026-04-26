# Scope (범위)

범위는 중괄호로 감싸진 부분을 의미한다.

기본적으로 어떤 범위 안에서 선언된 것은, 범위 밖에서 사용할 수 없다.

가령 다음과 같은 `for`문의 반복 변수가 그러하다.

```cs
static void Main(string[] args)
{
    int num = 10;

    for (int i = 0; i < 5; i++)
    {
        num++;
    }

    Console.WriteLine(i);    // Compile Error
    Console.WriteLine(num);
}
```

`for`문의 범위에서 선언된 변수 `i`는 `for`의 범위 밖에서 사용될 수 없다.

## Nested Scope (내포된 범위)

상위 범위에서 선언한 변수나 상수는 하위 범위에서 사용이 가능하다.

이전의 코드에서 `Main` 함수 범위에서 선언된 `num`이 `for`문 내부에서 사용된 것이 그러하다.

## Local Variable(지역변수)

기본적으로 함수 안에서 선언된 모든 것들은, 그 함수 내에서만 사용이 가능하다.  
이렇게 범위가 지정된 변수를 지역변수라고 한다.

가령, 다음의 코드에서 `num1`, `num2`, `sum은` 지역변수다.
이 지역변수들은 `Add` 함수의 범위에 속한다.

```cs
int Add(int num1, int num2)
{
    int sum = num1 + num2;
    return sum;
}
```

또한 기본적으로 함수 밖에 있는 변수나 상수는 사용할 수 없다.

가령, 다음 코드에서는 `Power`에서 계산된 `num1`은 `Square`에서 접근할 수 없다.

```cs
double Square(double number)
{
    Power(number, 2);
    return num1;        // Compile Error
}

double Power(double Base, int Exponent)
{
    int num1 = 1;

    for (int i = 0; i < Exponent; i++)
    {
        num1 *= Base;
    }

    return num1;
}
```

`num1`은 `Power`의 범위에 있다.  
`Square`의 범위가 아닌 아예 다른 범위에 존재하기 때문에 접근할 수 없다.

즉, `num1` 변수는 `Power` 함수 내에서 선언한 지역변수이므로, 다른 범위인 `Square`의 범위에서는 접근할 수 없다.

### 동일한 이름의 변수

그렇다면 다음과 같이 수정할 수 있다.

```cs
double Square(double num)
{
    Power(num, 2);
    return num;
}

double Power(double baseNum, int exponentNum)
{
    int num = 1;

    for (int i = 0; i < exponentNum; i++)
    {
        num *= baseNum;
    }

    return num;
}
```

두 함수 모두 변수의 이름으로 `num`을 사용하고 있다.  
이는, `Power` 함수에서 계산된 `num`을 `Square`에서 사용하고자 함을 전제한다.

하지만 결과적으로 `Square`이 반환하는 값은 `Square`가 전달받은 매개변수 `num`의 값이다.  
`Power`에서 선언된 반환값 `num`과 이름만 같을 뿐, 별개의 메모리 공간에 존재하는 다른 변수다.  
또한 `Power`에 전달하는 값 `num`은 `Power`의 매개변수 `baseNum`에 값이 복사될 뿐이며 동일한 변수가 아니다.

추가로, 범위가 겹치지 않으면 동일한 이름을 사용할 수 있음을 알 수 있다.
