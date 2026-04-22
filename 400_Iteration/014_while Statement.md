# `while` Statement

반복문 중 `while`에 대하여 다룬다.  

`while`은 주로 특정한 조건을 만족하는 동안 코드를 반복하기 위한 반복문이다.  
반복할 횟수가 반드시 정해져있는 것은 아니며, 의도한다면 무한 반복(infinite loop)도 가능하다.  

`while`문의 문법은 다음과 같다.

```cs
while (반복 조건식)
{
    반복할 코드
}
```

위 반복 조건식이 항상 `true`가 된다면, 반복할 코드가 계속 실행될 것이므로 무한 반복하게 된다.  

예를 들어, 어떤 FPS 게임에서 어떤 아이템이 있다고 가정하자.  
해당 아이템은, 1번 사격할 때 3발의 투사체가 발사된다고 한다.

이를 `while`문으로 구현하면 다음과 같다.

```cs
int count = 0;
const int PROJECTILE_COUNT = 3;

while (count < PROJECTILE_COUNT)
{
    (투사체 발사);
    count++;
}
```

위 `while`문은 다음과 같은 순서로 작동된다.  

1. **반복 조건 검사**  
    `count`의 값이 `PROJECTILE_COUNT`보다 작은지 검사한다.  
    반복 조건이 참일 경우, 내부 코드를 실행한다.  
    반복 조건이 거짓일 경우, 반복문을 탈출한다.  

2. **반복**  
    1번 단계로 실행 순서를 옮겨, 반복문을 진행한다.

즉, 위 코드는 `count`가 `0`에서 `3`까지 증가하여 총 3번의 투사체를 발사한다.  
그리고 조건 검사는 `count`가 `0`, `1`, `2`, `3`일 때 실행된다.  
마지막 검사에서 `count`가 `PROJECTILE_COUNT`보다 작지 않으므로 투사체 발사 로직이 실행되지 않고 반복문을 탈출하게 된다.  

## 무한 반복 (Infinite Loop)

예를 들어, 로그인 시스템을 생각해 볼 수 있다.  

간단한 로그인 시스템에서는 사용자가 계속 로그인 시도가 가능할 것이다.  
이는 곧, 사용자가 ID가 일치하지 않다면 계속 로그인 시도가 가능하는 것이다.  

```cs
string password = "qwer1234";
string userInput

while (true)
{
    userInput = (사용자 입력);

    if (userInput = password)
    {
        Debug.Log("Correct.");
        break;
    }

    Debug.Log("Wrong password.");
}
```

이때 주의할 점은, `break`는 오직 `switch/case`문과 반복문에 영향을 미치며 가장 가까운 구문을 탈출한다.  
따라서 `break`가 영향을 미치는 구문은 `while`문이다.
