

5. 명령어와 친해지기



추가 패키지



```
# apt-get install man
# apt-get install info

or

# apt install man
# apt install info

```



명령어의 정보 확인



type - 명령어의 이름이 어떻게 표시되는지 확인

which - 실행 프로그램의 위치 표시

man - 명령어의 man 페이지 표시

apropos - 적합한 명령어 리스트 표시

info - 명령어 정보 표시

whatis - 명령어에 대한 짧은 설명 표시

alias - 명령어에 별칭 붙이기





## 명령어

명령어 : /usr/bin 디렉토리처럼 실행 프로그램을 말한다.

C나 C++의 바이너리나 파이썬, node, 루비 같은 스크립트도 명령어다



쉘-빌트인(shell builtins) : 명령어는 쉘에 내장된 명령어



쉘 함수, 별칭(alias)도 명령어





## 명령어 확인

 type 명령어 타입 표시



명령어의 타입을 표시한다.

type command





type type

type ls

type cp



## which

실행 파일의 위치 표시



ls 의 위치를 표시한다.

which ls



cd 의 위치를 표시한다.

which cd





## 명령어 도움말 보기

help 쉘 빌트인 도움말 보기



```
help cd
mkdir --help

```



## man

프로그램 메뉴얼 표시

man program



| 섹션 | 내용                                       |
| ---- | ------------------------------------------ |
| 1    | 사용자   명령어                            |
| 2    | 커널   시스템 콜 API                       |
| 3    | C   라이브러리 API                         |
| 4    | 장치   노드 및 드라이버와 같은 특수 파일   |
| 5    | 파일   포맷                                |
| 6    | 스크린세이버와   같은 게임이나 미디어 파일 |
| 7    | 그외   여러 종류                           |
| 8    | 시스템   관리용 명령어                     |



man - 프로그램 메뉴얼 표시



man section search_term



man 5 passwd



## apropos - 적합한 명령어 찾기


```
apropos passwd

```







## whatis

간략한 명령어 정보 표시



```
whatis ls
```





## info - 프로그램 정보 표시


```
info ls

```



| 명령어                    | 실행                                       |
| ------------------------- | ------------------------------------------ |
| ?                         | 사용자   명령어                            |
| PAGE   UP 또는 BACKSPACE  | 커널   시스템 콜 API                       |
| PAGE   DOWN 또는 Spacebar | C   라이브러리 API                         |
| n                         | 장치   노드 및 드라이버와 같은 특수 파일   |
| p                         | 파일   포맷                                |
| u                         | 스크린세이버와   같은 게임이나 미디어 파일 |
| ENTER                     | 그외   여러 종류                           |
| q                         | 시스템   관리용 명령어                     |

   

## 별칭으로 나만의 명령어 만들기



command1; command2; commnad3...



```
cd /usr; ls; cd -

type test
type foo


alias name=‘string’

alias foo=‘cd /usr; ls; cd -’
foo
type foo
alias
```







# 6. 리다이렉션
입출력 방향 지정 (I/O리다이렉션)

강력한 파이프라인을 만들기 위해 명령어를 연결 할 수 있다.



cat - 파일 연결하기

sort - 텍스트 라인 정렬하기

uniq - 중복 줄을 알리거나 생략하기

wc - 각 파일의 개행 및 단 어 개수, 파일 바이트 출력하기

grep - 패턴과 일치하는 라인 출력하기

head - 파일의 첫 부분 출력하기

tail - 파일의 마지막 부분 출력하기

tee - 표준 입력을 읽고 표준 출력 및 파일에 쓰기





## 표준 입출력과 표준 오류
“모든 것은 파일이다" - 유닉스 정신



ls는 

표준 출력(stdout)이라고 불리는 특수한 파일에 명령 전송하고

표준 오류(stderr)라는 또다른 파일의 상태 메시지를 전송한다.

표준 입력(stdin)이라고 부르는 곳에서 입력 내용을 가져온다. (키보드에 연결된)



입출력 방향 지정(I/O 리다이렉션) 기능으로 입력과 출력의 방향을 변경 할 수 있다.





## 표준 출력 재지정

ls -l /usr/bin > ls-output.txt

ls -l ls-output.txt

less ls-output.txt

ls -l /bin/usr > ls-out.txt

ls -l ls-output.txt



파일 뒤에 이어쓰기

ls -l /usr/bin >> ls-output.txt



파일 디스크립터 2 는 표준 오류

ls -l /bin/usr 2> ls-error.txt



ls-error.txt 로 표준 오류를 보낸다.



### 표준 출력과 표준 오류를 한 파일로 재지정
ls -l /bin/usr > ls-output.txt 2>&1



파일 디스크립터 1 은 표준 출력



ls -l /bin/usr &> ls-output.txt

표준 출력과 표준 오류를 ls-output.txt 로 보낸다.



## 원치 않는 출력 제거

ls -l /bin/usr 2> /dev/null