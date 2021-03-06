---
layout: php
---
## 변수 유효 범위
<hr>

이번 장에서는 변수의 유효 범위(scope)에 대해서 알아보겠습니다. 변수의 유효 범위란 변수의 생성과 접근을 할 수 있는 범위를 말합니다.  

프로그램에서 변수를 생성, 사용 선언하게 되면 PHP는 메모리에 변수의 공간을 추가로 할당합니다. 이렇게 생성된 변수는 별도의 해제 작업을 하지 않는 경우 스크립트 실행 종료까지 유지하게 됩니다.  

변수의 유효 범위란 변수를 사용할 수 있는 프로그램 안에서의 코딩 공간이라고 이해하면 됩니다.
즉, 변수가 지배하는 땅과 같습니다.  

PHP에서는 변수의 영역에 대해서 다음과 같은 세 가지 타입을 가지고 있습니다.  
* Global	: 글로벌변수
* Local	: 지역변수
* Static	: 정적변수

<br>

### 학습내용
<hr>

* [글로벌변수](12.1)
* [로컬변수](12.2)
* [static 키워드](12.3)
* [글로벌 배열](12.4)
* [슈퍼변수](12.5)
* [$_SERVER](12.6)

<br><br>