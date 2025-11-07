
## 문제

```
def exam(num1, num2=2):

  print('a=', num1, 'b=', num2)

exam(20)
```

> a=20b=2


```
lst = [1, 2, 3]
dst = {i : i * 2 for i in lst}
s = set(dst.values())
lst[0] = 99
dst[2] = 7
s.add(99)
print(len(s & set(dst.values())))
```

> dst는 lst의 딕셔너리 형태
> dst = {1 : 2, 2 : 4, 3 : 6}
> s는 dst의 values, 즉 값만 추출
> s = [2, 4, 6]
> lst[0] = 99 대입
> lst = [99, 2, 3]
> dst[2] = 7         2에 해당하는 7 값 변경
> dst  = {1 : 2, 2 : 7, 3 : 6}
> s와 set(dst.values())의 교집합의 길이를 출력
> [2 4, 6] & [2, 7, 6]
> 따라서 2