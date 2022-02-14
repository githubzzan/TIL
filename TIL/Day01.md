# Git 특강 1일차 정리

# 1. CLI

GUI와 CLI의 정의

1. `GUI (Graphic User Interface)` : 그래픽을 통해 사용자와 컴퓨터가 상호 작용하는 방식
2. `CLI (Command Line Interface)` : 터미널을 통해 사용자와 컴퓨터가 상호 작용하는 방식

> Interface(인터페이스) 인터페이스란 원래 서로 다른 개체끼리 맞닿아 있는 면을 뜻합니다. 여기에서는 사용자와 컴퓨터가 서로 소통하는 접점이라고 이해하도록 합시다

## 경로

### (1) 루트, 홈 디렉토리

1. **루트 디렉토리 (Root Directory, `/`)**
   - 모든 파일과 폴더를 담고 있는 최상위 폴더입니다.
   - Windows의 경우 보통은 `C 드라이브`를 의미합니다.
2. **홈 디렉토리 (Home Directory, `~`)**
   - `Tilde(틸드)`라고도 부르며, 현재 로그인 된 사용자의 홈 폴더를 의미합니다.
   - Windows의 경우 `C:/사용자(Users)/현재 사용자 계정`을 의미합니다.
   - Mac의 경우 `/Users/현재 사용자 계정`을 의미합니다.

> 💡 **폴더 vs 디렉토리**

> 폴더와 디렉토리는 거의 같은 의미로 사용됩니다. 따라서 의미의 구분이 무의미합니다. 세부적으로 따져보자면, 윈도우 탐색기에서의 특수 폴더 들(ex. 네트워크 환경, 내컴퓨터 등)은 폴더이지만 디렉토리는 아닙니다. 따라서 폴더가 디렉토리보다 넓은 개념이라고 할 수는 있겠습니다.

</aside>

### (2) 절대 경로와 상대 경로

1. 절대 경로

    : 루트 디렉토리부터 목적 지점까지 거치는 모든 경로를 전부 작성한 것

   - 윈도우 바탕 화면의 절대 경로 `C:/Users/kyle/Desktop`

2. 상대 경로

    : 현재 작업하고 있는 디렉토리를 기준으로 계산된 상대적 위치를 작성한 것

   - 현재 작업하고 있는 디렉토리가 `C:/Users` 라고 한다면
   - 윈도우 바탕 화면으로의 상대 경로는 `kyle/Desktop` 이 됩니다.
   - 간결해서 좋지만, 현재 작업하고 있는 디렉토리가 변경 되면 상대 경로도 변경됩니다.
   - `./` : 현재 작업하고 있는 폴더를 의미합니다.
   - `../` : 현재 작업하고 있는 폴더의 부모 폴더를 의미합니다.

# 2. Visual Studio Code

> Visual Studio Code 왜 쓰나요? - Vscode는 마이크로소프트에서 개발한 코드 에디터의 한 종류입니다. - Windows, Mac, Linux를 모두 지원합니다. - 기존 개발 도구들 보다 가볍고 빠르다는 장점이 있습니다. - 전 세계에서 사랑 받는 굉장한 점유율의 에디터입니다. - Extension을 통해 다양한 기능을 설치할 수 있어서, 무한한 확장성을 가집니다. - 게다가 무료로 사용 가능합니다.

### Extensions란?

- `익스텐션`이란 기본 기능에서 확장하여 추가적인 기능을 가능하게 하는 일종의 `플러그인`입니다.

- vscode를 열고 왼쪽 메뉴바에서 `블럭 모양의 아이콘`을 통해 익스텐션 창을 열 수 있습니다.

  > 처음부터 모든 기능을 갖추면 되지, 왜 익스텐션을 쓰나요? 
  >
  > 물론, 처음부터 모든 기능을 갖춘다면 일일히 익스텐션을 설치 하지 않아도 될 것입니다. 하지만 그만큼 불필요한 기능도 많아서 필요 이상으로 에디터가 무거워집니다. vscode는 사용자가 필요한 기능을 익스텐션을 통해 추가 설치 할 수 있도록 지원하여 가벼우면서도 다양한 작업을 할 수 있는 환경을 제공하고 있습니다.

# 3. Markdown 배우기



제목(headings) #의 갯수
# 제목1
## 제목2
### 제목3
#### 제목4
##### 제목5
###### 제목6

2. 순서 (list)
- 순서가 없는 목록1
- 순서가 없는 목록2
  - 서브 목록 1
  - 서브 목록 2
    - 서브 서브 목록 1

1. 순서가 있는 목록1
2. 순서가 있는 목록2
   1. 서브 목록1
      1. 서브 서브 목록1

3. 강조

- 기울임 : *글자* _글자_   글자 앞뒤로 *,_

  - 굵게 : **글자** __글자__  글자 앞뒤로 *,_ 2개씩

    - 취소 : ~~글자~~  글자 앞뒤로 ~2개씩


      4. 소스 코드
      - 한 줄 코드 (인라인 코드)
    
        `print("Hello world!")`


      - 여러 줄 코드 (블록 코드)
    
        ```python
        for i in range(10):
        	print(i)
        ```
    
      5. 표 (table)
    
         | 동물 이름 | 다리 개수 | 종     |
         | --------- | --------- | ------ |
         | 사자      | 4개       | 포유류 |
         | 토끼      | 4개       | 포유류 |
         | 앵무새    | 2개       | 조류   |
         |           |           |        |


      6. 수평선
      -, *, _ 세번 이상 반복하면 가능하다. 

# 실습



#  Python



## 1. 개요

<img src="Day01.assets/image-20220112135351938.png" alt="image-20220112135351938" style="zoom:33%;" />

![image]

파이썬(Python)은 1990년 암스테르담의 귀도 반 로섬(Guido Van Rossum)이 개발한 인터프리터 언어이다. 귀도는 파이썬이라는 이름을 자신이 좋아하는 코미디 쇼인 "몬티 파이썬의 날아다니는 서커스(Monty Python’s Flying Circus)"에서 따왔다고 한다.

> 인터프리터 언어란 한 줄씩 소스 코드를 해석해서 그때그때 실행해 결과를 바로 확인할 수 있는 언어이다.



## 2. 특징

1. 파이썬은 인간다운 언어이다. 아래 코드는 쉽게 해석된다.

​	`if 4 in [1,2,3,4]: print("4가 있습니다")`

​	만약 4가 1, 2, 3, 4 중에 있으면 "4가 있습니다"를 출력한다. 라고 말이다.

 	2. **파이썬은 간결하다**

``` python
#simple.py
languages = ['python', 'perl', 'c', 'java']

for lang in languages:
	if lang in ['python', 'perl']:
		print("%6s need interpreter" % lang)
	elif lang in ['c', 'java']:
		print("%6s need compiler" % lang)
	else:
		print("should not reach here")
```

3. 공식문서가 자세히 제공된다.

   [파이썬 공식문서 링크](https://docs.python.org/3/)



# 4. Git 기초



## 	1. Git 환경설정 (최초 1번만 하면 됨)

​		git config --global user.name edukyle
​		git config --global user.email edukyle.hphk@gmail.com

​		git config --global --list



## 	2. git 로컬 저장소 만들기

​		git init



## 	3. git 파일 상태 보기

​		git status



## 	4.  Working Directory -> Staging Area

​		git add a.txt

​		Staging Area -> Commits
​		git commit -m "commit message"



## 	5. git 커밋 목록 보기

​		git log
​		git log --oneline
​		git log -p



# 5. Github

​	[2] 원격 저장소 (Remote Repository)

> 여태 까지는 내 컴퓨터라는 한정된 공간에 있는 로컬 저장소에서만 버전 관리를 진행했습니다. 이제는 Github의 원격 저장소를 이용해 내 컴퓨터의 로컬 저장소를 다른 사람과 `공유`해봅시다. Git의 주요 목적 중 하나인 `협업`을 위해 로컬 저장소와 원격 저장소의 연동 방법을 학습합니다.

### (1) Github에서 원격 저장소 생성

![화면 오른쪽 상단 더하기(+) 버튼을 누르고 New repository를 클릭합니다.](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/55e28914-796f-487f-9ce1-972cf15cc1d1/%EA%B7%B8%EB%A6%BC3.png)

화면 오른쪽 상단 더하기(+) 버튼을 누르고 New repository를 클릭합니다.

![저장소의 이름, 설명, 공개 여부를 선택하고 Create repository를 클릭합니다. (체크 박스는 건드리지 않습니다!)](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/40d4c341-35df-4cf7-8586-83afe060d56c/%EA%B7%B8%EB%A6%BC4.png)

저장소의 이름, 설명, 공개 여부를 선택하고 Create repository를 클릭합니다. (체크 박스는 건드리지 않습니다!)

### (2) 로컬 저장소와 원격 저장소 연결

1. 원격 저장소가 잘 생성되었는지 확인 후, 저장소의 주소를 복사합니다.

   ![그림5.png](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/798d21e0-9c40-4995-b5ed-fc77b9e75bb1/%EA%B7%B8%EB%A6%BC5.png)

2. 기존에 실습 때 만들었던 홈 디렉토리의 TIL 폴더로 가서 vscode를 엽니다.

3. git init을 통해 TIL 폴더를 로컬 저장소로 만들어줍니다.

   ```bash
   kyle@KYLE MINGW64 ~/TIL
   $ git init
   Initialized empty Git repository in C:/Users/kyle/TIL/.git/
   ```

4. **git remote**

   - 로컬 저장소에 원격 저장소를 `등록, 조회, 삭제`할 수 있는 명령어

   1. **원격 저장소 등록**

      `git remote add <이름> <주소>` 형식으로 작성합니다.

      ```bash
      $ git remote add origin <https://github.com/edukyle/TIL.git>
      
      [풀이]
      git 명령어를 작성할건데, remote(원격 저장소)에 add(추가) 한다.
      origin이라는 이름으로 <https://github.com/edukyle/TIL.git라는> 주소의 원격 저장소를
      ```

   2. **원격 저장소 조회**

      `git remote -v` 로 작성합니다.

      ```bash
      $ git remote -v
      origin  <https://github.com/edukyle/TIL.git> (fetch)
      origin  <https://github.com/edukyle/TIL.git> (push)
      
      add를 이용해 추가했던 원격 저장소의 이름과 주소가 출력됩니다.
      ```

   3. **원격 저장소 연결 삭제**

      `git remote rm <이름>` 혹은 `git remote remove <이름>` 으로 작성합니다.

      > 로컬과 원격 저장소의 연결을 끊는 것이지, 원격 저장소 자체를 삭제하는 게 아닙니다.

      ```bash
      $ git remote rm origin
      $ git remote remove origin
      
      [풀이]
      git 명령어를 작성할건데, remote(원격 저장소)와의 연결을 rm(remove, 삭제) 한다.
      그 원격 저장소의 이름은 origin이다.
      ```

### (3) 원격 저장소에 업로드

- 실습 때 작성했던 TIL 파일을 Github 원격 저장소에 업로드 해보겠습니다.
- **정확히 말하면, 파일을 업로드하는 게 아니라 커밋을 업로드 하는 것입니다!**
- 따라서 먼저 로컬 저장소에서 커밋을 생성해야 원격 저장소에 업로드 할 수 있습니다.

1. **로컬 저장소에서 커밋 생성**

   ```bash
   # 현재 상태 확인
   
   $ git status
   On branch master
   
   No commits yet
   
   Untracked files:
     (use "git add <file>..." to include in what will be committed)
           day1.md
   
   nothing added to commit but untracked files present (use "git add" to track)
   ```

   ```bash
   $ git add day1.md
   ```

   ```bash
   $ git commit -m "Upload TIL Day1"
   [master (root-commit) f3d6d42] Upload TIL Day1
    1 file changed, 0 insertions(+), 0 deletions(-)
    create mode 100644 day1.md
   ```

   ```bash
   # 커밋 확인
   
   $ git log --oneline
   f3d6d42 (HEAD -> master) Upload TIL Day1
   ```

2. **git push**

   - 로컬 저장소의 커밋을 원격 저장소에 업로드하는 명령어
   - `git push <저장소 이름> <브랜치 이름>` 형식으로 작성합니다.
   - `-u` 옵션을 사용하면, 두 번째 커밋부터는 `저장소 이름, 브랜치 이름`을 생략 가능합니다.

   ```bash
   $ git push origin master
   
   [풀이]
   git 명령어를 사용할건데, origin이라는 이름의 원격 저장소의 master 브랜치에 push 한다.
   
   ------------------------------------------------
   
   $ git push -u origin master
   이후에는 $ git push 라고만 작성해도 push가 됩니다.
   ```

