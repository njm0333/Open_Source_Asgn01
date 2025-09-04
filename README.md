# Open_Source_Asgn01
Open_Source_Software Asgn_01 by Noh Jeong Min


> 유닉스 명령어 정리 _ 3
- stty erase 지울키 + enter
     지움키 백스페이스로
 - less -n /etc/passwd 
	less 형식으로 passwd파일을 보여줘, 그리고 less로 보여줄 때 끊는키는 q
- stty -a 를 하면 stop키가 무슨 키로 설정되어 있는지도 볼 수 있어
- cat :  txt파일 열기
	 cat -n hello.txt : n속성 붙여서 각 줄에 번호를 붙여줌
	 cat -n /etc/passwd | more : passwd파일을 줄을 붙여서 보여주는데, more형식으로
- more : more 형식으로 페이지별 파일 열기
       끊는키는 ctrl c
- less : less 형식으로 파일보기
    끊는키는 q
- pg : 파일의 내용을 한 화면씩 출력
- head : 앞 10줄만 보여줘
- head /pwd/passwd -3 : 앞 3줄만 -3이라는걸로 할 수 있음
- tail : 뒤 10줄만 보여줘
- cat -n /etc/passwd | head -100 | tail -10
- cat /etc/passwd | sort | more
	정렬해서 more로 보여줘
- tail -f /var/
	-f라는 건 마지막값만 보여주고 최신화되면 최신화 된 값을 계속 이어서 보여줌

---


> 복사하기

```bash
cp [원본 파일/디렉토리] [타겟 파일/디렉토리]
```
- 타겟에 내용을 넣겠다는거
- `cp file1.txt file2.txt`는 `file1.txt`를 복사하여 `file2.txt`라는 이름으로 저장
- `cp file1.txt /home/user/`는 `file1.txt`를 `/home/user/` 디렉토리에 복사
- `cp -r folder1 folder2`는 `기

- rm 이 지우는 명령어

- rm -i : 확인 후 삭제
- rm -f : 무조건 삭제
- rm -r : 디렉토리 지우는건데 안에 내용이 있든 없든 강제로 지움

> 실제 활용문들

- mkdir dir1 : dir1 디렉토리 만들고
- echo hi > hi.txt : txt파일 만들고
- cp hi.txt dir1 : 만든 파일을 dir1 디렉토리에 넣었는데
- rm -r dir1 : dir1에 파일이 있는데도 경고없이 그냥 지움

---

> 파일 이동

```bash
mv [원본 파일/디렉토리] [타겟 파일/디렉토리]
```
- 이름을 바꾸거나, 이름바꿈이 함축하는 의미인 디렉토리를 변경하기(같은 파티션에서만)
- `mv file1.txt file2.txt`는 `file1.txt`를 `file2.txt`로 **이름을 변경**합니다.
- `mv file1.txt /home/user/`는 `file1.txt`를 `/home/user/` 디렉토리로 **이동**합니다.
- `mv folder1 folder2`는 `folder1` 디렉토리를 `folder2`라는 이름으로 **변경**하거나 **이동**합니다.
- mv 파일 파일 : 이름을 바꿈
- mv 파일 디렉토리 : 파일을 옮김

> 실제 활용문들

- echo hi > hi.txt
- mv hi.txt hello.txt
	이렇게 이름을 바꿈


어떻게보면 mv는 이름을 바꾸는 명령어야. 
파일을 이동하는것도 어떻게 보면 파일의 주소 이름을 바꾸는 거니까
예시를 들어 설명해보자면

/user/unix113/hi.txt
에서

/user/unix113/dir1/hi.txt 
이렇게 바뀐다는 의미

---

> 하드링크, 소프트링크
> ==하드 링크는 같은 파티션에서만 쓸 수 있다는 치명적인 단점. 하지만 같은 파티션이면 빠르긴 해==

- 파일은 하드링크 1개 
- 디렉은 하드링크 2개



> 기본 명령어

```bash
ln [원본 파일] [링크 파일]
ln -s [원본 파일] [소프트링크 파일]
ls -l : 링크 명령어는 아니지만, data-value에 할당된 I-Node의 갯수
ls -i : 링크 명령어는 아니지만, data-value에 할당된 I-Node의 raw값을 보여줌
```


> 하드링크

- **설명**: 하드링크는 원본 파일의 데이터 블록을 직접 참조. 동일한 파일 시스템 내에서만 사용
- **특징**:
    - 원본 파일과 하드링크 파일은 동일한 **아이노드 번호**를 공유
    - 원본 파일을 삭제해도 하드링크 파일은 여전히 데이터에 접근할 수 있습니다.
    - 하드링크만 같은 파티션에서 쓰는거니까 아이노드 번호가 동일!!
    - 디렉토리에는 기본적으로 하드링크가 2개 존재한다는거임임.
- **예시**:
    ```bash
    ln hello.txt hello_ref.txt
    ```
    `hello.txt`의 하드링크 `hello_ref.txt`를 만드는거!!


> 소프트링크 (심볼릭 링크)

- **설명**: 소프트링크는 원본 파일의 경로를 참조하는 별도의 파일. Windows의 바로가기랑 비슷함
- **특징**:
    - 원본 파일과 소프트링크 파일은 서로 다른 **아이노드 번호**
    - 원본 파일이 삭제되거나 경로가 변경되면 소프트링크는 깨짐. dangling 발생
    - 크기가 작고, 다른 파일 시스템 간에도 사용가능함.
- **예시**:
    ```bash
    ln -s /export/home/unix113/hello.txt hello_softref.txt
    ```
    `hello.txt`를 가리키는 소프트링크 `hello_softref.txt`를 생성한다는거



> 하드링크 / 소프트링크를 이해하기 위한 I-Node

I-Node란? : 
data블럭의 앞에 딱 붙어있는 컴퓨터가 처리하기 위한 데이터값
I-Node::Data-value 이런 느낌으로

- ls -i 를 했을 때
아이노드 번호는 같은데 이름만 두 개 있는거야. 그러니까 데이터를 저장하기 위한 데이터 저장공간은 하나만 차지하는거고 그 데이터를 가리키는 하드링크만 두 개를 만든거지
C++로 이해한다고 하면, 참조자를 선언했다고 이해함

대신 복사기능인 cp를하면 ls -i 를 했을 때 두 자료의 아이노드 번호가 달라. 
즉, 데이터 블럭에서 서로 다른 공간을 차지하고 있다는거고 서로 다른 자료라는거야.




---

> touch
> 파일 생성 및 시간 변경

- touch newfile.txt : 빈 파일 생성
- touch -a example.txt : 접근 시간만 변경
- touch -m example.txt : 수정 시간만 변경
- touch -c example.txt : 파일이 없을 경우 생성하지 않음
- touch -t 202504151230 example.txt : 특정 시간으로 설정 (형식: [[CC]YY]MMDDhhmm[.ss])
	 CC : 세기
	 세기를 안넣으면 CC까지 YY를 표기하는데 사용할 수 있어서
	 YYYY MM DD HH MM 형식으로 표현가능
- touch -r sourcefile.txt targetfile.txt :  파일의 시간 정보를 복사



