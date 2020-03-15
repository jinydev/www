## ln - 링크 생성하드링크

ln file link



소프트 링크 (심볼릭 링크)

ln -s item link



## 하드 링크 생성



```
ln fun fun-hard
ln fun dir1/fun-hard
ln fun dir2/fun-hard

ls -l

ls -li  
아이노드 확인
아이노드(inode)라고 불리는 디스크 블록체인을 하나 할당하고 이름 영역과 연결한다.

```





## 심볼릭 링크 생성



```
하드링크는 파일만 참조할 수 있고 디렉토리를 참조할 수 없다. (단점)

ln -s fun fun-sym
ln -s ../fun dir1/fun-sym
ln -s ../fun dir2/fun-sym

ls -l dir1

ln -s /root/playground/fun dir1/fun-sym
ln -s dir1 dir1-sym
ls -l

```

