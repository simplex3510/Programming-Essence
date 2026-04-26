# Pass by, Call by

함수 호출과 인자 전달에 대한 내용을 다룬다.

함수를 호출 할 때 인자를 전달한다.  
이때, 전달한 값이 바뀜을 기대하는 경우도 있다.

다음의 코드에서 그것을 의도했다고 가정한다.

```cs
double Square(double num)
{
    Power(num, 2);
    return num;
}

double Power(double num, int exponentNum)
{
    for (int i = 1; i < exponentNum; i++)
    {
        num *= num;
    }

    return num;
}
```

`Square`함수에서 `num`을 `Power`로 전달하고, `num`의 값이 바뀜을 기대하여 그대로 반환하고 있다.

하지만 실질적으로는 `Square`가 전달받은 `num`이 `Square`에서 그대로 반환된다.

## Pass by Value (값에 의한 전달)

위 코드가 의도한 바는, `Square`함수의 변수 `num`을 원본으로서 전달하고, 바뀐 값을 반환 것이다.

하지만 해당 `num`을 전달받은 `Power`함수에서는 `baseNum` 매개변수에 `num` 변수의 값이 복사되어 전달된다.
즉, 값을 전달할 인자 `num`과 전달받은 매개변수`num`은 서로 다르다.

따라서 원본인 `Square`의 `num`에 영향을 미치지 않는다.

정리하자면, 피호출자(receiver)인 `Power`의 매개변수 값이 변경되어도 호출자(caller)의 인자에 반영되지 않는다.

---

의도한 값을 얻기 위해 다음과 같이 `Power`의 반환값을 `Square`에서 지역변수에 저장하여 수정할 수 있다.

```cs
double Square(double num)
{
    int result = Power(num, 2);
    return result;
}

double Power(double num, int exponentNum)
{
    for (int i = 1; i < exponentNum; i++)
    {
        num *= num;
    }

    return num;
}
```

하지만 이는 원본 `num`이 변경되는 것을 의도함에서 벗어나, 의도한 값을 얻은 것뿐이다.

## Pass by Reference (참조에 의한 전달)

C#에서는 원본을 전달함을 `ref` 키워드를 사용한다.  
매개변수 또는 인자 앞에 `ref`를 표기하여 사용할 수 있다.

따라서 의도한대로, 원본을 전달하는 코드는 다음과 같이 수정할 수 있다.

```cs
double Square(double num)
{
    Power(ref num, 2);
    return num;
}

double Power(ref double num, int exponentNum)
{
    for (int i = 1; i < exponentNum; i++)
    {
        num *= num;
    }

    return num;
}
```

`Square`에서 `Power`를 호출할 때 `num`을 `ref`로서 전달하고 있으므로, 원본이 전달된다.  
`Power`에서는 매개변수로 `num`을 받을 때 `ref`로서 전달받고 있으므로, 원본이 전달된다.

전달된 `num`은 `Power`의 연산에 의해서 원본이 변경되고, 이를 `Square`에서 반환한다.

이렇듯, `ref` 키워드로 수식한 인자를 전달하면 원본이 전달된다.  
이는 곧 원본 변수와 인자, 즉 매개변수가 서로 같음을 의미한다.

정리하자면, 피호출자(receiver)인 `Power`의 매개변수 값이 변경되면 호출자(caller)의 인자에 반영된다.

### `unsafe` and Pointer(포인터)

위 `ref` 키워드를 포인터 개념으로 바꾸어 표현할 수 있다.
근본적으로, `ref`는 포인터를 사용한다.

따라서 포인터 개념을 사용한 코드는 다음과 같이 수정될 수 있다.

```cs
unsafe double Square(double num)
{
    Power(&num, 2);
    return num;
}

unsafe double Power(double* num, int exponentNum)
{
    for (int i = 1; i < exponentNum; i++)
    {
        *num *= *num;
    }

    return *num;
}
```

C#에서는 포인터를 직접적으로 다룰 수 없으며, 이를 위해 `unsafe` 키워드를 사용한다.  
이를 통해 어떤 함수에서 포인터를 다룸을 컴파일러에게 알린다.

`Power`함수를 호출할 때, `Square`함수의 매개변수 `num`의 주소값을 전달한다.

`Power`함수는 매개변수 `num`을 `double*`형으로 전달받는다.  
즉, `double`형 변수의 주소값을 전달받는다.

`Power`의 내부 연산에서 `*num`으로 주소값에 접근하여, 원본 `num`에 접근한다.  
따라서 원본 `num`의 값이 변경된다.

## 핵심은 원본의 변경 유무

값에 의한 전달은 원본을 전달하지 않고 복사된 값을 전달한다.  
따라서 원본 자체에는 영향을 미치지 않는다.

하지만 참조에 의한 전달은 원본을 전달한다.
따라서 원본 자체에 영향을 충분히 미친다.
