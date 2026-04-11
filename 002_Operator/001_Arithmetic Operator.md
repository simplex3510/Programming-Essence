# Operator (연산자)
연산자(Operator)는 데이터를 어떻게 처리할지 지시하는 약소된 기호라고 할 수 있다.  
이때 연산자는 피연산자, 즉 연산의 대상을 반드시 하나 이상 가져야 한다.

# Arithmetic Operator (산술 연산자)
산술 연산자는 일반적으로 수행하는 사칙연산을 수행하는 연산자를 의미한다.  
더하기와 빼기, 곱하기와 나누기를 수행하는 연산자다.
```cs
sbyte num1 = 2;
sbyte num2 = 10;

// result1 = 12
sbyte result1 = num1 + num2;

// result2 = 1111 1000 = -8
sbyte result2 = num1 - num2;
// result2 = 1111 1000 = 248
byte result2 = (byte)num1 - (byte)num2;

// result3 = 20
sbyte result3 = num1 * num2;

// result4 = 0
int result4 = num1 / num2;
// result4 = 0.0
double result4 = num1 / num2;
// result4 = 0.2
double result4 = num1 / (double)num2;
```

`result2`의 연산에서, `Unsigned Type`인 타입의 값을 연산했을 때 음수를 기대하면 안된다.  
이러한 경우에는 `Underflow`가 발생하여 의도하지 않은 값이 발생할 수도 있다.

또한 `result4`의 연산에서, 두 자료형이 모두 정수형일 경우에도 의도하지 않은 값이 발생될 수 있다.  
따라서 실수값을 기대하는 경우에는, 실수형 타입으로 형 변환을 명시하여 연산의 과정에서 실수값을 사용하도록 해야 한다.