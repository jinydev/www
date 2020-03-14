
## LS

간단 목록 확인

ls



디렉토리의 목록 확인

ls /usr



여러 디렉토리 목록 확인

ls ~ /usr



디테일한 목록 확인

ls -l



### 명령어 옵션과 명령인자
t : 파일 수정 시간에 따른 결과 정렬

ls -lt



--reverse : 정렬결과를 역순으로 보여준다.

ls -lt --reverse

​    urces/app/



### 주로 많이 사용되는 ls 옵션


| 옵션 | long   옵션      | 설명                                                         |
| ---- | ---------------- | ------------------------------------------------------------ |
| -a   | --all            | 모든   파일 보기 (숨김 파일도 표시)                          |
| -d   | --directory      | 해당   디렉토리 자체가 아닌 디렉토리 내용 자체를 표시한다.   |
| -F   | --classify       | 지시   문자를 추가한다. (ls -F /)                            |
| -h   | --human-readable | -l   옵션과 함께 사용하여 파일 크기를 사람이 인식하기 쉬운 형태로 표시 |
| -l   |                  | 자세한   정보를 출력                                         |
| -r   | --reverse        | 출력   결과를 역순으로 표시. (일반적으로 ls 는 알파벳 오름차순으로 표시) |
| -s   |                  | 파일   크기 순으로 정렬                                      |
| -t   |                  | 파일   시간 순으로 정렬                                      |

   

### long 포맷으로 출력 결과 보기



```
ls -l /usr/bin

-rwxr-xr-x 1 root root   30904 Jan 18  2018 true
-rwsr-xr-x 1 root root   26696 May 16 10:41 umount
-rwxr-xr-x 1 root root   35032 Jan 18  2018 uname
-rwxr-xr-x 2 root root    2301 Apr 28  2017 uncompress
-rwxr-xr-x 1 root root  133792 Jan 18  2018 vdir
-rwxr-xr-x 1 root root   30800 May 16 10:41 wdctl
-rwxr-xr-x 1 root root     946 Dec 30  2017 which
lrwxrwxrwx 1 root root       8 Jan 31  2018 ypdomainname -> hostname
-rwxr-xr-x 1 root root    1937 Apr 28  2017 zcat
-rwxr-xr-x 1 root root    1777 Apr 28  2017 zcmp

```





### ls 자세히 보기 정보


| 항목           | 의미                         |
| -------------- | ---------------------------- |
| -rw-r--rwx     | 파일   접근 권한을 보여준다. |
| 1              | 하드   링크의 수를 보여준다. |
| root           | 파일   소유자의 사용자 이름  |
| root           | 파일을   소유한 그룹 이름    |
| 2018           | 파일   크기 (바이트 단위)    |
| Dec   30  2017 | 파일   마지막 수정 날짜      |
| zcat           | 파일명                       |

​    



## file - 명령어로 파일 타입 확인
파일을 타입을 확인할 수 있다.



file filename



file lazy_dog.txt 

lazy_dog.txt: ASCII text

