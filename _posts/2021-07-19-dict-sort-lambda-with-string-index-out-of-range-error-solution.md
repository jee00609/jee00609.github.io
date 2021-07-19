---
title: "Dictionary 의 Sort (sorted) 함수에서 Python Error - IndexError: string index out of range 해결"

categories:
  - python
tags: 
  - Error
  - Sort
last_modified_at: 2021-07-19
---

Python 관련하여 동기 언니가 IndexError: string index out of range 가 발생한 Dictionary Sort 문제를 가지고 왔다.

다른 친구들과 여러 이야기를 나누면서 Python 의 Sort 방식에 대한 자료를 모았고 해결책도 찾게 됬다.

Sort 문법의 lambda 와 관련된 문제였는데 메모할 가치가 있다고 생각하여 포스팅한다.

## Dictionary 의 sort 기본 형식

   ```ruby
sorted(d.items(), key=lambda x: x[1])
   ```

value 값으로 정렬하고 싶을 때 자주 사용하는 문법이다.

이 떄 lambda 뒤에 써있는 x[1] 이 무엇인지 제대로 생각하지 않고 살아왔던 것 같다.

아래 코드의 에러를 해결하면서 고찰을 해보기로 하겠다.

## IndexError: string index out of range

   ```ruby
def solution():

    dict={'A':3,'C': 5,'B' :8 , 'E':10, 'F':13} 

    print("dict : ",dict)
    print("dict.items : ",dict.items())
    print("\n")
    new_dict1=sorted(dict.items(), key=lambda x :x[1], reverse=True)

#     에러발생
    new_dict2=sorted(dict ,key=lambda x:x[1], reverse=True)
    print("new dict 1 : ",new_dict1)
    print("new dict 2: ",new_dict2)


solution()

# 출력
# dict :  {'A': 3, 'C': 5, 'B': 8, 'E': 10, 'F': 13}
# dict.items :  dict_items([('A', 3), ('C', 5), ('B', 8), ('E', 10), ('F', 13)])


# ---------------------------------------------------------------------------
# IndexError                                Traceback (most recent call last)
# <ipython-input-13-1754e7f51535> in <module>
#      13 
#      14 
# ---> 15 solution()

# <ipython-input-13-1754e7f51535> in solution()
#       8     new_dict1=sorted(dict.items(), key=lambda x :x[1], reverse=True)
#       9 
# ---> 10     new_dict2=sorted(dict ,key=lambda x:x[1], reverse=True)
#      11     print("new dict 1 : ",new_dict1)
#      12     print("new dict 2: ",new_dict2)

# <ipython-input-13-1754e7f51535> in <lambda>(x)
#       8     new_dict1=sorted(dict.items(), key=lambda x :x[1], reverse=True)
#       9 
# ---> 10     new_dict2=sorted(dict ,key=lambda x:x[1], reverse=True)
#      11     print("new dict 1 : ",new_dict1)
#      12     print("new dict 2: ",new_dict2)

# IndexError: string index out of range

   ```

위의 코드에서 new_dict2 를 보자

dict.items() 를 사용하지 않고 dict 를 사용했기에 key 값을 정렬한다.

그것 이외에는 new_dict1 과 차이점이 없지만 에러가 발생했다.

이유가 무엇일까


## sorted(key=lambda: …) 에서 key=lambda x :x[1] 에 대한 이해

먼저 lambda 에 대해 이해해봐야 한다.

개인적으로 lambda 는 코드 내에서 여러번 사용되지 않을 이름 없는 함수라고 생각하면서 이야기를 적어 나갈 것이다.

   ```ruby

In [1]: f00 = lambda x: x/2

In [2]: f00(10)
Out[2]: 5.0

In [3]: (lambda x: x/2)(10)
Out[3]: 5.0

In [4]: (lambda x, y: x / y)(10, 2)
Out[4]: 5.0

In [5]: (lambda: 'amazing lambda')() # func with no args!
Out[5]: 'amazing lambda'

# Example 1

# mylist = [3, 6, 3, 2, 4, 8, 23]
In [8]: sorted(mylist, key=lambda x: x % 2 == 0)

# Quick Tip: The % operator returns the *remainder* of a division
# operation. So the key lambda function here is saying 
# "return True if x divided by 2 leaves a remainer of 0, else False". 
# This is a  typical way to check if a number is even or odd.

Out[8]: [3, 3, 23, 6, 2, 4, 8]  
# python 에서는 Flase True 순으로 정렬된다.

   ```

위의 코드에서 볼 때 'key=' 는 한 번에 하나의 요소(예: some_list의 e)를 통해 목록을 반복하면서 현재 요소를 키 인수로 지정된 함수에 전달하고 이를 사용하여 다음을 알려주는 변환된 목록을 만드는 것을 알 수 있다.

또한 x 는 sorted에서 key 앞에 들어올 인자를 이야기 한다는 것을 알 수 있다.

그렇다면 IndexError: string index out of range 가 발생한 이유 또한 알 수 있다.

즉 sort 에서 lambda 의 문법 형식은

   ```ruby
sorted ([list 혹은 dic], key = lambda x: [key로 지정하고 싶은 요소])
   ```

## IndexError: string index out of range 해결

IndexError: string index out of range 났던 이유는 dict 에 들어가있던 key 값의 길이가 단 1이었기 때문에 발생한 것이다.

key=lambda x :x[1] 을 하기 위해 x 를 봤더니 dict 의 key 값에 들어간 값들은 모두 A,C,B,E,F 처럼 단 한글자로 이루어져 있었고 이로 인해 에러가 났다.

이를 고치려면 대략 두가지의 방법이 있다.

key 값들의 길이를 변경하거나, x[0] 으로 변경한다.

   ```ruby
# key 값들의 길이를 변경

def solution():

    dict={'Ac':3,'Ca': 5,'Be' :8 , 'Ef':10, 'Fa':13} 

    print("dict : ",dict)
    print("dict.items : ",dict.items())
    print("\n")
    new_dict1=sorted(dict.items(), key=lambda x :x[1], reverse=True)

    new_dict2=sorted(dict ,key=lambda x:x[1], reverse=True)
    print("new dict 1 : ",new_dict1)
    print("new dict 2: ",new_dict2)


solution()
   ```

   ```ruby
# x[0] 으로 변경

def solution():

    dict={'A':3,'C': 5,'B' :8 , 'E':10, 'F':13} 

    print("dict : ",dict)
    print("dict.items : ",dict.items())
    print("\n")
    new_dict1=sorted(dict.items(), key=lambda x :x[1], reverse=True)

    new_dict2=sorted(dict ,key=lambda x:x[0], reverse=True)
    print("new dict 1 : ",new_dict1)
    print("new dict 2: ",new_dict2)


solution()
   ```



## 참고 사이트

매우 이해하기 쉬운 설명과 예제를 써준 유저분께 감사하며 사이트 주석을 달아놓는다...

[Syntax behind sorted(key=lambda: …)](https://stackoverflow.com/questions/8966538/syntax-behind-sortedkey-lambda)

[[python] python의 sort함수에 사용되는 lambda에 대한 이해](https://engineer-mole.tistory.com/94)

