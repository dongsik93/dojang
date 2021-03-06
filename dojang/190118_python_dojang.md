## 38장. 예외처리 사용하기

### try except 사용하기



```python
try:
    실행할 코드
except:
    예외가 발생했을 때 처리하는 코드
```

```python
y = [10, 20, 30]
 
try:
    index, x = map(int, input('인덱스와 나눌 숫자를 입력하세요: ').split())
    print(y[index] / x)
except ZeroDivisionError:   
    # 숫자를 0으로 나눠서 에러가 발생했을 때 실행됨
    print('숫자를 0으로 나눌 수 없습니다.')
except IndexError:           
    # 범위를 벗어난 인덱스에 접근하여 에러가 발생했을 때 실행됨
    print('잘못된 인덱스입니다.')
```

### else & finally

```python
try:
    실행할 코드
except:
    예외가 발생했을 때 처리하는 코드
else:
    예외가 발생하지 않았을 때 실행할 코드
finally:
    예외 발생 여부와 상관없이 항상 실행할 코드
```

### 예외 발생 시키기

#### raise

```python
def three_multiple():
    try:
        x = int(input('3의 배수를 입력하세요: '))
        if x % 3 != 0:                                
            # x가 3의 배수가 아니면
            raise Exception('3의 배수가 아닙니다.')    
            # 예외를 발생시킴
        print(x)
    except Exception as e:                            
        # 함수 안에서 예외를 처리함
        print('three_multiple 함수에서 예외가 발생했습니다.', e)
        raise    
        # raise로 현재 예외를 다시 발생시켜서 상위 코드 블록으로 넘김
 
try:
    three_multiple()
except Exception as e:                                
    # 하위 코드 블록에서 예외가 발생해도 실행됨
    print('스크립트 파일에서 예외가 발생했습니다.', e)
```



## 39장. 이터레이터 사용하기

- 이터레이터(iterator, 반복자)는 값을 차례대로 꺼낼 수 있는 객체(object)이다.

### 반복가능한 객체

- 문자열, 리스트, 딕셔너리, 세트 : 요소가 여러개 들어있고, 한 번에 하나씩 꺼낼 수 있다

### for와 반복 가능한 객체

- for에 range(3)을 사용했다면, 먼저 range에서 `__iter__`로 이터레이터를 얻는다
- 그리고 반복할 때마다 이터레이터에서 `__next__` 로 숫자를 꺼내서 i에 저장하고 지정된 숫자 3이 되면 StopIteration을 발생시켜서 반복을 끝낸다.

![img](https://dojang.io/pluginfile.php/13952/mod_page/content/2/039001.png)

### 시퀀스 객체와 반복 가능한 객체의 차이

- 반복 가능한 객체는 시퀀스 객체를 포함한다
- 요소의 순서가 정해져 있고 연속적으로 이어져 있으면 시퀀스 객체, 요소의 순서와 상관없이 요소를 한번에 하나씩 꺼낼 수 있으면 반복가능한 객체이다.
- 리스트, 튜플, range, 문자열은 반복가능한 객체이면서 시퀀스 객체
- 딕셔너리와 세트는 반복가능한 객체이지만 시퀀스 객체는 아니다

### 이터레이터 만들기

`__iter__` , `__next__` 메서드를 구현해서 직접 이터레이터를 만들어 보기

```python
class 이터레이터이름:
    def __iter__(self):
        코드
    def __next__(self):
        코드
```

```python
class Counter:
    def __init__(self, stop):
        self.current = 0   
        # 현재 숫자 유지, 0부터 지정된 숫자 직전까지 반복
        self.stop = stop    # 반복을 끝낼 숫자
 
    def __iter__(self):
        return self         
    # 현재 인스턴스를 반환
 
    def __next__(self):
        if self.current < self.stop:   
            # 현재 숫자가 반복을 끝낼 숫자보다 작을 때
            r = self.current           
            # 반환할 숫자를 변수에 저장
            self.current += 1           
            # 현재 숫자를 1 증가시킴
            return r                    
        	# 숫자를 반환
        else:                           
            # 현재 숫자가 반복을 끝낼 숫자보다 크거나 같을 때
            raise StopIteration         
            # 예외 발생
 
for i in Counter(3):
    print(i, end=' ')
```



### 인덱스로 접근할 수 있는 이터레이터 만들기

```python
class 이터레이터이름:
    def __getitem__(self, 인덱스):
        코드
```

```python
class Counter:
    def __init__(self, stop):
        self.stop = stop
 
    def __getitem__(self, index):
        if index < self.stop:
            return index
        else:
            raise IndexError
 
print(Counter(3)[0], Counter(3)[1], Counter(3)[2])
 
for i in Counter(3):
    print(i, end=' ')
```

### iter, next 함수 활용

- iter는 객체의 `__iter__` 메서드를 호출
- next는 객체의 `__next__` 메서드를 호출

```python
# iter
import random
it = iter(lambda : random.radint(0,5), 2)
# iter(호출가능한 객체, 반복을 끝낼 값)
```

```python
# next
it = iter(range(3))
next(it, 10)
>>> 0
next(it, 10)
>>> 1
# next(반복가능한 객체, 기본값)
```





