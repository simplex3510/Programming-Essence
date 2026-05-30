# C언어 포인터 배열 복습 및 논리력 강화 문제

## [문제 1] 포인터 배열의 기본 구조 이해

**다음 C언어 코드의 실행 결과로 올바른 출력 값을 순서대로 작성하고, 포인터 배열 `arr`의 각 요소가 무엇을 저장하고 있는지 설명하시오.**

```c
#include <stdio.h>

int main() {
    int a = 10, b = 20, c = 30;
    int *arr[3] = {&a, &b, &c};
    
    printf("%d ", *arr[0]);
    printf("%d ", *arr[1]);
    printf("%d\n", *arr[2]);
    
    return 0;
}

```

---

## [문제 2] 포인터 배열과 값의 변경

**다음 코드가 실행된 후 화면에 출력되는 `a`와 `b`의 값을 쓰고, `*arr[1] = 50;` 연산이 메모리에 미친 영향에 대해 서술하시오.**

```c
#include <stdio.h>

int main() {
    int a = 5, b = 15;
    int *arr[2] = {&a, &b};
    
    *arr[0] = 25;
    *arr[1] = 50;
    
    printf("a = %d, b = %d\n", a, b);
    return 0;
}

```

---

## [문제 3] 포인터 배열을 이용한 문자열 관리

**다음 프로그램의 실행 결과를 쓰고, 일반 2차원 char 배열(`char str[3][10]`)과 비교했을 때 포인터 배열을 활용한 문자열 관리의 메모리적 장점을 서술하시오.**

```c
#include <stdio.h>

int main() {
    char *fruits[3] = {"Apple", "Banana", "Strawberry"};
    
    for(int i = 0; i < 3; i++) {
        printf("%s ", fruits[i]);
    }
    printf("\n");
    return 0;
}

```

---

## [문제 4] 포인터 배열의 연산과 주소 추적

**다음 코드에서 포인터 연산과 인덱스 접근이 일어날 때, 최종적으로 출력되는 값을 기술하시오.**

```c
#include <stdio.h>

int main() {
    int arr1[2] = {100, 200};
    int arr2[2] = {300, 400};
    
    int *ptr_arr[2] = {arr1, arr2};
    
    printf("%d ", ptr_arr[0][1]);
    printf("%d\n", *(ptr_arr[1] + 0));
    
    return 0;
}

```

---

## [문제 5] 문자열 포인터 배열의 특정 문자 접근 (심화)

**다음 코드의 출력을 분석하여 최종적으로 화면에 찍히는 문자를 쓰고, `*fruits[2]`와 `*(fruits[1] + 3)`이 각각 의미하는 바를 설명하시오.**

```c
#include <stdio.h>

int main() {
    char *fruits[3] = {"Apple", "Banana", "Orange"};
    
    printf("%c", *fruits[2]);
    printf("%c\n", *(fruits[1] + 3));
    
    return 0;
}
