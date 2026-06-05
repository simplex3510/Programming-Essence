## 프로그래밍기능사 실기 대비 C언어 모의 평가

### [문제 1] 다음 C언어 프로그램의 실행 결과를 쓰시오.

```c
#include <stdio.h>

int main() {
    int a = 12;
    int b = 5;
    int c = 3;
    int result = a / b + a % b * c;
    
    printf("%d", result);
    return 0;
}

```

---

### [문제 2] 다음은 1부터 10까지의 정수 중 홀수의 합을 구하는 C언어 프로그램이다. 프로그램의 실행 결과로 '25'가 출력되도록 빈칸 [  ①  ]에 들어갈 알맞은 제어 조건을 쓰시오.

```c
#include <stdio.h>

int main() {
    int sum = 0;
    for (int i = 1; i <= 10; i++) {
        if ([  ①  ]) {
            continue;
        }
        sum += i;
    }
    
    printf("%d", sum);
    return 0;
}

```

---

### [문제 3] 다음 C언어 프로그램의 실행 결과를 쓰시오.

```c
#include <stdio.h>

int main() {
    int arr[5] = {3, 5, 7, 9, 11};
    int sum = 0;
    
    for (int i = 0; i < 5; i += 2) {
        sum += arr[i];
    }
    
    printf("%d", sum);
    return 0;
}

```


---

### [문제 4] 다음 C언어 프로그램의 실행 결과를 쓰시오.

```c
#include <stdio.h>

int main() {
    int a = 20;
    int b = 12;
    
    while (a != b) {
        if (a > b) {
            a -= b;
        } else {
            b -= a;
        }
    }
    
    printf("%d", a);
    return 0;
}

```

---

### [문제 5] 다음 C언어 프로그램의 실행 결과를 쓰시오.

```c
#include <stdio.h>

int main() {
    char str[] = "NICE";
    char *p = str;
    
    p += 2;
    
    printf("%c%s", *p, p);
    return 0;
}

```
