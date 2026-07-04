# 🐍 Python 리스트 레벨업: 삽입·삭제·검색·정렬·컴프리헨션 중급 10선

### [문제 1] [삽입] insert() 메서드로 특정 위치에 원소 넣기

`numbers` 리스트의 인덱스 2번 자리에 숫자 `99`를 삽입하여 `[10, 20, 99, 30, 40]`이 되도록 빈칸에 알맞은 메서드와 인자를 채워 넣으세요.

```python
numbers = [10, 20, 30, 40]

# 인덱스 2번 자리에 99 삽입하기
numbers.________(________)

print(numbers)
# 출력 예시: [10, 20, 99, 30, 40]

```

---

### [문제 2] [삭제] remove()와 pop()의 차이 이해하기

`items` 리스트에서 값 `'banana'`를 지우는 코드와, 맨 마지막 원소인 `'cherry'`를 꺼내어 변수에 저장하는 코드를 각각 완성하세요.

```python
items = ['apple', 'banana', 'orange', 'cherry']

# 1. 값을 지정하여 'banana' 삭제하기
items.remove(________)

# 2. 맨 마지막 원소를 꺼내서 popped_item 변수에 저장하기
popped_item = items.pop(________)

print(items)        # 출력 예시: ['apple', 'orange']
print(popped_item)   # 출력 예시: cherry

```

---

### [문제 3] [검색] index() 메서드로 위치 찾기

리스트에 특정 데이터가 몇 번째 인덱스에 있는지 알아내려고 합니다. `members` 리스트에서 `'Chulsoo'`의 인덱스 위치를 찾아 출력하는 빈칸을 완성하세요.

```python
members = ['Younghee', 'Cheolsoo', 'Minsu', 'Suzy']

# 'Cheolsoo'가 위치한 인덱스 번호 구하기
target_index = members.________('Cheolsoo')

print(target_index)
# 출력 예시: 1

```

---

### [문제 4] [검색] in 연산자로 포함 여부 확인하기

`if` 조건문과 `in` 연산자를 사용하여, `inventory` 리스트 안에 `'gold'`가 존재하면 `"보물을 발견했습니다!"`를 출력하고, 없으면 `"아무것도 없습니다."`를 출력하는 코드를 완성하세요.

```python
inventory = ['sword', 'shield', 'potion', 'gold']

# 'gold'가 리스트 안에 있는지 확인하는 조건문 작성
if ________:
    print("보물을 발견했습니다!")
else:
    print("아무것도 없습니다.")

```

---

### [문제 5] [정렬] sort()와 sorted()의 결정적 차이

원본 리스트 자체를 정렬하여 바꾸는 메서드와, 원본은 그대로 두고 정렬된 새로운 리스트를 반환하는 함수를 구별하여 빈칸을 알맞게 채우세요.

```python
origin_A = [4, 1, 3, 2]
origin_B = [4, 1, 3, 2]

# 1. origin_A 자체를 제자리에서 정렬하기 (원본이 변경됨)
origin_A.________()

# 2. origin_B는 보존하고, 정렬된 새 리스트를 new_list에 담기
new_list = ________(origin_B)

print(origin_A)  # 출력 예시: [1, 2, 3, 4]
print(origin_B)  # 출력 예시: [4, 1, 3, 2] (원본 유지)
print(new_list)  # 출력 예시: [1, 2, 3, 4]

```

---

### [문제 6] [정렬] 내림차순(역순)으로 정렬하기

정수 리스트를 값이 큰 순서대로(내림차순) 정렬하고 싶습니다. 정렬 기능을 사용할 때 어떤 옵션을 추가해야 하는지 생각하여 빈칸을 완성하세요.

```python
scores = [75, 90, 85, 60, 100]

# 내림차순 정렬 옵션 지정하기
scores.sort(________)

print(scores)
# 출력 예시: [100, 90, 85, 75, 60]

```

---

### [문제 7] [컴프리헨션] 기초적인 스퀘어 리스트 생성

1부터 5까지의 숫자가 들어있는 `nums` 리스트를 바탕으로, 각 숫자의 제곱값(square)들을 원소로 가지는 새로운 리스트를 리스트 컴프리헨션(한 줄 코드)으로 생성하세요.

```python
nums = [1, 2, 3, 4, 5]

# 리스트 컴프리헨션을 사용해 [1, 4, 9, 16, 25] 만들기
squares = [________ for x in nums]

print(squares)
# 출력 예시: [1, 4, 9, 16, 25]

```

---

### [문제 8] [컴프리헨션] 필터링 조건(if) 추가하기

주어진 단어 리스트에서 **글자 수(길이)가 5글자 이상인 단어들만** 골라내어 새로운 리스트를 만들려고 합니다. 리스트 컴프리헨션 내부의 조건문 빈칸을 채우세요.

```python
words = ['apple', 'cat', 'banana', 'dog', 'elephant', 'fox']

# 5글자 이상인 단어만 필터링하는 리스트 컴프리헨션 완성
long_words = [w for w in words if ________]

print(long_words)
# 출력 예시: ['apple', 'banana', 'elephant']

```

---

### [문제 9] [종합] 검색 후 안전하게 삭제하기

리스트에서 특정 값을 삭제할 때, 만약 그 값이 리스트에 없다면 에러(`ValueError`)가 발생합니다. 안전한 프로그램 작성을 위해, **먼저 `in` 연산자로 값의 존재 여부를 확인한 후, 존재할 때만 삭제(`remove`)하는 논리**를 조건문으로 구현하세요.

```python
fruits = ['apple', 'orange', 'grape']
target = 'banana'

# target이 fruits에 존재할 때만 삭제하는 안전한 코드 구현


print(fruits)
# 'banana'가 없으므로 에러 없이 ['apple', 'orange', 'grape']가 그대로 출력되어야 합니다.

```

---

### [문제 10] [종합] 문자열 리스트를 정수 리스트로 변환하기 (컴프리헨션)

파일이나 사용자로부터 입력받은 데이터는 숫자가 아닌 문자열 형태(`'1'`, `'2'`)일 때가 많습니다. 리스트 컴프리헨션과 형변환 함수(`int()`)를 조합하여 문자열 리스트를 완벽한 정수형 리스트로 변환하는 코드를 완성하세요.

```python
str_numbers = ['10', '20', '30', '40']

# 리스트 컴프리헨션으로 정수 리스트 생성
int_numbers = [________ for ________ in str_numbers]

print(int_numbers)
# 출력 예시: [10, 20, 30, 40]
# 데이터 타입 확인 (정상 변환 시 True 출력)
print(type(int_numbers[0]) == int) 

```
