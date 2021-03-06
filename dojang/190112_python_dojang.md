## 24. 문자열 응용하기

### 문자열 바꾸기

- replace('바꿀 문자열', '새문자열')

```python
'Hello, world!'.replace('world','Python')
>>> 'Hello, Python!'
```

- maketrans('바꿀 문자', '새문자')
- translate('테이블')

```python
table = str.maketrans('aeiou','12345')
'apple'.translate(table)
>>> '1pp12'
# maketrans로 변환 테이블을 만든 뒤 translate()를 사용
```

### 문자열 분리 & 연결하기

- split()

```python
'apple pear grape pineapple orange'.split()
>>> ['apple', 'pear', 'grape', 'pineapple', 'orange']
# 공백을 기준으로 문자열을 분리하여 리스트로 만듬

'apple pear grape pineapple orange'.split(',')
# 콤마로도 가능
```

- join(리스트)

```python
''.join(['apple', 'pear', 'grape', 'pineapple', 'orange'])
>>> 'apple pear grape pineapple orange'
# 공백 ''에 join을 사용하여 각 문자열 사이에 공백이 들어가도록 함
```

### 대 & 소문자 변환

- 소문자를 대문자로 : upper()

```python
'python'.upper()
>>> 'PYTHON'
```

- 대문자를 소문자로 : lower()

```python
'PYTHON'.lower()
>>> 'python'
```

### 공백 삭제

- 왼쪽공백 삭제 : lstrip()

```python
'	Python 	'.lstrip()
>>> 'Python   '
```

- 오른쪽 공백 삭제 : rstrip()

```python
'	Python    '.rstrip()
>>> '	Python'
```

- 양쪽 공백 삭제 : strip()

```python
'	Python    '.strip()
>>> 'Python'
```

### 특정문자 삭제

- 왼쪽 특정문자 삭제

```python
', python.'.lstrip(',.')
>>> ' python'
```

- 오른쪽 특정문자 삭제

```python
', python.'.rstrip(',.')
>>> ', python'
```

- 양쪽의 특정문자 삭제

```python
', python.'.strip(',.')
>>> ' python'
```

### 구두점을 간단하게 삭제하기

- string모듈의 punctuation에는 모든 구두점이 들어 문자열 양쪽의 모든 구두점을 간단하게 삭제할 수 있다

```python
import string
', python.'.strip(string.punctuation)
>>> ' python'

string.punctuation
>>> '!"#$%&\'()*+,-./:;<=>?@[\\]^_`{|}~'
# punctuation에 들어있는 모든 구두점

', python.'.strip(string.punctuation + ' ')
# 구두점에 공백을 연결해서 공백까지 삭제

', python.'.strip(string.punctuation).strip()
# 메서드 체이닝을 활용해서 구두점, 공백까지 삭제
# 메서드 체이닝은 메소드의 연결
```

### 문자열 정렬

- 왼쪽 정렬 : ljust(길이)

```python
'python'.ljust(10)
>>> 'python    '
# 문자열을 지정된 길이로 만든 뒤 왼쪽으로 정렬해 남은 공간은 공백으로 채움
```

- 오른쪽 정렬

```python
'python'.rjust(10)
>>> '    python'
# 오른쪽 정렬 후 남은 공간을 공백으로 채움
```

- 가운데 정렬

```python
'python'.center(10)
>>> '  python  '
# 가운데 정렬 후 남는 공간을 공백으로 채움
```

### 메서드 체이닝

- 메서드를 계속 연결해서 호출

```python
'python'.rjust(10).upper()
# 문자열을 오른쪽으로 정렬한 뒤 대문자로 바꿈
```

### 문자열 왼쪽에 0 채우기

```python
'35'.zfill(4)
>>> '0035'
'3.5'.zfill(6)
>>> '0003.5'
# 지정된 길이에 맞춰서 숫자 앞에 0을 채움
```

### 문자열 위치 찾기

- find(), rfind()

- 문자열에서 특정 문자열을 찾아서 인덱스를 반환하고, 문자열이 없으면 -1 반환

```python
'apple pineapple'.find('pl')
>>> 2
# 같은 문자열이 여러개일 경우 처음 찾은 문자열의 인덱스를 반환
```

- index()
- 왼쪽에서붜 특정 문자열을 찾아서 인덱스를 반환, 문자열이 없으면 에러 발생

```python
'apple pineapple'.index('pl')
>>> 2
```

- 문자열 개수 세기

```python
'apple pineapple'.count('pl')
>>> 2
```



### 서식지정자(format specifier)

- `'%s' % '문자열'` : 문자열 중간에 다른 문자열을 넣기

```python
'I am %s.' % 'james'
>>> 'I am james.'
# 문자열 안에 %s를 넣고 그 뒤에 %를 붙인 뒤 'james'를 지정해주면 바뀜

name = 'maria'
'I am %s' % name
# 변수를 지정할 수도 있음
```

- `'%d' % 숫자`  : 문자열 안에 숫자 넣기
- `'%f' % 숫자`  & `'%.자릿수f' % 숫자 `  : 소수점 표현하기

```python
'I am %d years old.' % 20
>>> 'I am 20 years old.'

'%f' % 2.3
>>> 2.30000
'%.2f' % 2.3
>>> 2.30
'%.3f' % 2.3
>>> 2.300
```

- `%길이s` : 문자열 오른쪽 정렬하기 
- `%-길이s` : 문자열 왼쪽 정렬하기

```python
'%10s' % 'python'
>>> '    python'
# 문자열 길이를 10으로 만든 뒤 지정문자열을 넣고 오른쪽으로 정렬
'%-10s' % 'python'
>>> 'python    '
# 왼쪽 정렬
```

- 문자열 안에 값 여러개 넣기

```python
'Today is %d %s. ' % (3, 'April')
>>> 'Today is 3 April. '
# 서식 지정자 개수와 변수 개수도 똑같이 맞춰주어야 함
```

### format 메서드

```python
'Hello, {0} {2} {1}'.format('Python', 'Script', 3.6)
>>> 'Hello, Python 3.6 Script'
```

![img](https://dojang.io/pluginfile.php/13716/mod_page/content/4/024006.png)



- { }에 인덱스 대신 이름을 지정하기

```python
'Hello, {language} {version}'.format(language='Python', version=3.6)
>>> 'Hello, Python 3.6'

```

- 3.6버전 이후 문자열 포매팅에 변수 사용하기

```python
language = 'Python'
version = 3.6
f'Hello, {language} {version}'
>>> 'Hello, Python 3.6'
```

- format 메서드로 문자열 정렬하기

```python
'{:<10}'.format('python')
>>> 'python    '
f"{'python':<10}"
>>> 'python    '
# 왼쪽정렬
```

- 금액에서 천단위로 콤마 넣기 : `format(숫자, '.')`

```python
format(1493500, ',')
>>> '1,493,500'

'%20s' % format(1493500, ',')
>>> '          1,493,500'
# 길이 20, 오른쪽으로 정렬
```

### raw문자열

- 문자열 앞에 r, R을 붙이면 raw문자열이 됨
- 이스케이프 시퀀스를 그대로 저장할 때 사용,  `\` 를 `\\`  로 두번 쓰지 않고 한번만사용

```python
print(r"1\n2\n3\n")
>>> 1\n2\n3\n
```

