## 29장. 함수 사용하기

### 장점

- 코드의 용도를 구분할 수 있다
- 코드를 재사용 할 수 있다
- 실수를 줄일 수 있다

```python
def 함수이름():
    코드
```

### 함수 작성 & 호출순서

- 함수를 먼저 호출하면 함수가 정의되지 않았다는 에러가 발생
- 실행순서는 파이썬 스크립트 실행 - 함수호출 - 함수실행 - 출력 - 함수종료 - 파이썬 스크립트 종료

### 매개변수(parameter)

- 함수에 값을 받으려면 ()(괄호)안에 변수 이름을 지정해주면 되는데 이를 매개변수라 함
- 함수를 호출할 때 넣는 값을 인수(argument)라고 부름

### 함수 값 반환

- return 을 통해 반환
- return으로 여러 개 반환하면 실제로는 튜플이 반환된다



## 30장. 함수에서 위치 인수와 키워드 인수 사용하기

### 위치 인수

- 함수에 인수를 순서대로 넣는 방식
- 즉 인수의 위치가 정해져 있다

```python
print(10, 20, 30)
>>> 10 20 30 
# 10 20 30 순으로 넣었으므로 출력도 10 20 30 으로 출력됨
```

### 언패킹

- 리스트나 튜플 앞에 *를 붙이면 언패킹이 된다

```python
x = [10, 20, 30]
print_numbers(*x)
>>> 10 20 30 
```

### 가변인수 함수

```python
def 함수이름(*매개변수):
    코드
```

- 같은 함수에 인수 한개를 넣을 수 있고, 열 개를 넣을 수도 있다
- 관례적으로 매개변수는 args로 사용한다

```python
def print_numbers(*args):
    for arg in args:
        print(arg)
        
# 넣은 숫자 개수만큼 출력된다
```

### 고정인수와 가변인수 함께 사용하기

```python
def print_number(a, *args):
    print(a)
    print(args)
    
# 고정인수와 가변인수를 함께 사용할 때는 다음과 같이 고정 매개면수를 먼저 지정하고, 그 다음 매개변수에 *를 붙여주면 됩니다.
```

### 키워드 인수

- 인수에 이름(키워드)을 붙이는 기능, 키워드=값 형식으로 사용

```python
personal_info(name="홍길동", age=30, address="서울시 용산구 이촌동")
```

### 딕셔너리 언패킹

- 딕셔너리 앞에 **를 붙여서 함수에 넣어준다
- 키-값 쌍 형태로 저장되어 있기 때문에 **두개 넣어줌

### 키워드 인수를 사용하는 가변인수 함수

```python
def 함수이름(**매개변수):
    코드
```

- 매개변수 이름은 관례적으로 kwargs로 사용한다

### 위치 인수와 키워드 인수를 함께 사용하기

```python
def custom_print(*args, **kwargs):
    print(*args, **kwargs)
    
custom_print(1,2,3, sep=":", end="")
# kwargs는 항상 가장 뒤쪽에
```

### 매개변수의 초기값

- 함수를 만들 때 매개변수에 초기값을 지정하면 함수를 호출할 때 해당 인수를 비워두고 호출할 수 있다

```python
def 함수이름(매개변수=값):
    코드
```

### 순수함수 & 비순수 함수

- 순수함수 : 함수의 실행이 외부 상태에 영향을 끼치지 않는 함수

```python
def add(a,b):
    return a + b
# 함수 실행이 외부 상태에 영향을 끼치지 않음
```

- 비순수 함수(수정자 함수) : 함수의 실행이 외부 상태에 영향을 끼치는 함수

```python
num_list = [1, 2, 3]

def append_number(n):
    num_list.append(n)
# 함수 외부에 있는 num_list의 상태에 따라 함수 실행에 영향을 끼침
```





## 31장. 재귀함수

자기 자신을 호출하는 것

RecursionError에 유의해야 한다

### 재귀함수로 팩토리얼 구하기

```python
def factorial(n):
    if(n==1):
        return 1
    return factorial(n-1)*n
```



## 32장. 람다 표현식

람다 표현식으로 익명 함수를 만드는 방법

### 람다 표현식으로 함수 만들기

- lambda 매개변수들 : 식

```python
def plus_ten(x):
    return x + 10

# 람다 표현식으로 만들기
plus_ten = lambda x: x + 10
# 람다 표현식은 이름이 없는 함수이기 때문에 람다로 만든 익명 함수를 호출하려면 다음과 같이 람다 표현식을 변수에 할당해 주면 된다
```

### 람다 표현식 자체를 호출하기

- (lambda 매개변수들 : 식) (인수들)

```python
(lambda x: x + 10)(1)
>>> 11
```

- 람다 표현식 안에서는 새 변수를 만들 수 없기 때문에 반환값 부분은 변수 없이 식 한줄로 표현할 수 있어야 한다. 변수가 필요한 코드일 경우에는 def함수로 작성해야함

### 람다 표현식을 인수로 사용하기

```python
def plus_ten(x):
    return x + 10

list(map(plus_ten, [1,2,3]))
```

```python
# lambda
list(map(lambda x: x + 10, [1, 2, 3]))
```

### 람다 표현식에 조건식 사용하기

- lambda 매개변수들 : 식1 if 조건식 else 식2

```python
a = [1,2,3,4,5,6,7,8,9,10]
list(map(lambda x: str(x) if x%3 == 0 else x, a))
```

- else가 없으면 오류 발생, elif 는 사용할 수 없음



## 33. 클로저 사용하기

### 변수의 사용 범위

- 전역변수(global variable) : 함수를 포함하여 스크립트 전체에서 접근할 수 있는 변수
- 전역범위(global scope) : 전역변수에 접근할 수 있는 범위

![img](https://dojang.io/pluginfile.php/13866/mod_page/content/2/033001.png)



- 지역변수(local variable) : 변수를 만든 함수 안에서만 접근 할 수 있다

- 지역범위(local scope) : 지역변수를 접근할 수 있는 범위

  ![img](https://dojang.io/pluginfile.php/13866/mod_page/content/2/033002.png)

- 함수 안에서 전역변수의 값을 변경하려면 `global` 이라는 키워드를 사용해야 한다

```python
x = 10
def foo():
    global x
    x = 20
    print(x)
    
foo()
print(x)
>>> 20
>>> 20

# 전역변수를 global로 수정했기 때문에 
```

### 네임스페이스(namespace)

- 파이썬에서 변수는 네임스페이스에 저장된다
- locals() 함수를 사용하면 현재 네임스페이스를 딕셔너리 형태로 출력할 수 있다

### 함수 안에서 함수 만들기

```python
def print_hello():
    hello = "hello, world!"
    def print_message():
        print(hello)
    print_message()
    
print_hello()

# 두 함수가 실제로 동작하려면 바깥쪽의 print_hello를 호출해 주어야 안쪽 함수도 실행됨
```

### 지역 변수의 범위

- 안쪽 함수 print_message에서는 바깥쪽 함수 print_hello의 지역변수를 사용할 수 있다.  즉 바깥쪽 함수의 지역변수는 그 안에 속한 모든 함수에서 접근할 수있다

![img](https://dojang.io/pluginfile.php/13867/mod_page/content/2/033003.png)

### 지역변수 변경하기

- 파이썬에서는 함수에서 변수를 만들면 항상 현재 함수의 지역변수가 된다

```python
def A():
    x = 10
    def B():
        x = 20
        
    B()
    print(x)
    
A()
>>> 10
# 겉으로 보면 바깥쪽 함수 A의 지역변수x를 변경하는 것 같지만, 실제로는 안쪽 함수 B에서 이름이 같은 지역변수 x를 새로만들게 되기 때문에 10이 출력된다
```

- 현재 함수의 바깥쪽에 있는 지역변수의 값을 변경하려면 `nonlocal` 키워드를 사용해야 한다

```python
def A():
    x = 10
    def B():
        nonlocal x
        x = 20
    
    B()
    print(x)
    
A()
>>> 20
# nonlocal은 현재 함수의 지역변수가 아니라는 뜻이며 바깥쪽 함수 지역변수를 사용
```

### nonlocal이 변수를 찾는 순서

```python
def A():
    x = 10
    y = 100
    def B():
        x = 20
        def C():
            nonlocal x
            nonlocal y
            x = x + 30
            y = y + 300
            print(x)
            print(y)
        C()
    B()
 
A()

>>> 50
>>> 400

# nonlocal은 가까운 함수부터 지역변수를 찾고, 지역변수가 없으면 계속 바깥쪽으로 나가서 찾는다
```

### global로 전역변수 사용하기

- 함수가 몇 단계든 상관없이 global 키워드를 사용하면 무조건 전역변수를 사용한다

```python
x = 1
def A():
    x = 10
    def B():
        x = 20
        def C():
            global x
            x = x + 30
            print(x)
        C()
    B()
 
A()
>>> 31
```

### 클로저(closure)

- 함수를 둘러싼 환경(지역변수, 코드 등)을 계속 유지하다가 함수를 호출할 때 다시 꺼내서 사용하는 함수를 클로저라고 한다.

```python
def calc():
    a = 3
    b = 5
    def mul_add(x):
        return a * x + b    
    return mul_add  
# mul_add를 만든 뒤에는 이 함수를 바로 호출하지 않고 return으로 함수 자체를 반환한다( 함수를 반환할 때는 함수 이름만 반환해야 하며, ()(괄호)를 붙이면 안됨)

c = calc()
print(c(1), c(2))
# c에 저장된 함수가 클로저
```

![img](https://dojang.io/pluginfile.php/13868/mod_page/content/2/033004.png)

















