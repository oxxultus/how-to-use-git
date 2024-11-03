
# Create an easy-to-view terminal
> 운영체제 기본 터미널을 사용하는것 보다 가독성이 뛰어나고 편리하다.


## How to download on mac
- [mac]()

## How to download on windows
> 윈도우 에서도 리눅스 기반으로 터미널을 사용할 것으로 바꿀 예정
- [Winddow](https://github.com/oxxultus/how-to-use-git/blob/f2e44bd099b0e3c7eba459de9e909482786c85c4/How%20to%20download%20on%20windows.md)



# Git Start
1. [Git ](https://git-scm.com/downloads)으로 이동해서 운영체제에 맞는 Git 을 설치한다.

## Start Setup
- Git config check (Git 설정 확인)
```Shell
git config --list
```

- git config set user.name (Git 닉네임 설정)
```Shell
git config user.name "설정할 이름"
```

- git config set user.email (Git 이메일 설정)
```Shell
git config user.email "본인 이메일"
```

- git config set core.autocrlf (Git 운영체제간의 줄바꿈 통일)
```Shell
// Window
git config core.autocrlf true

// Mac
git config core.autocrlf input
```

- git config set core.editor (Git  기본 에디터를 vscode 로 설정)
	1. `--wait` 옵션은 `vscode` 실행 중 인 경우 `terminal` 을 잠시 사용할 수 없고, 수정이 완료가 된다면 `terminal` 입력이 가능하게 하는 옵션 중 하나이다.
	2. . 만약 `--wait` 옵션을 지운다면, vscode 사용 중 `terminal`사용이 가능합니다.
```Shell
git config --global core.editor "code --wait"
```

- git diff to vscode (Git 글로벌 설정을 기본에디터로 실행)
```Shell
git config --global -e


#==========================================
# add [diff], [difftool]
# in .gitcofig
[diff] 
	tool = vscode
[difftool "vscode"]
	cmd = code --wait --diff $LOCAL $REMOTE
#==========================================
```


## First Step.
### Create Git
- Git 을 처음 사용할 때 사용하는 명령어 입니다. (초기화 작업)
	1. Terminal 을 이용해 Git을 사용하기 위한 directory 로 이동한다.
	2. `git init` 명령어를 사용한다.
```Shell
git init
```

### Delete Git
- Git 을 더 이상 사용하지 않을 때 삭제하는 명령어 입니다.
	1. Terminal 을 이용해 Git 폴더가 위치한  directory 로 이동한다.
	2. `rm -rf .git`  명령어를 사용한다.
	3. Git은 .git 설정 파일이 사라지면 삭제된다.
```Shell
# rm -rf 는 파일을 삭제하는 리눅스 명령어 입니다. 
rm -rf .git
```

### Excluding file tracking (.gitignore)
- echo 명령어에 대해 간단하게 설명할게요.
```Shell
# 파일이름.확장자 라는 파일이 없을 때는 생성하며 있다면 내용을 덮어쓰게 됩니다.
# 간단하게 설명하면 파일 덮어쓰기이다.
echo "코드,문자열 등등" > 파일이름.확장자

# 파일이름.확장자 라는 파일이 없을 때는 생성하며 있다면 파일이름.확장자 파일에 내용을 추가하게 됩니다.
# 간단하게 설명하면 기존파일은 지워지지 않고 새롭게 추가된 기존파일이다.
echo "코드, 문자열 등등" >> 파일이름.확장자
```

- .gitignore에 추가하면 해당 파일은 더이상 Git에 업로드 되지 않는다.
```Shell
# 추가 하고 싶은 파일 확장자
echo *.확장자 >> .gitignore 

# 폴더명에 위치한 파일은 Git 에서 체크하지 않는다.
echo 폴더명/ >> .gitignore 

# 폴더명에 위치한 확장자를 가진 모들 파일을 체크 하지 않는다.
echo 폴더명\*.확장자 >> .gitignore 

# 해당 명령어로 vi 편집기로 작성해도 됩니다.
vi ~/.gitignore # vi 편집기 열기
source ~/.gitignore # 수정내용 저장

# 해당 명령어로 cscode 를 열어서 수정해도 됩니다.
code ~/.gitignore
source ~/.gitignore
```
> .git 파일에서 직접 .gitignore 를 수정해도 상관없다.

## Second Step.
### Working Directory
- 파일의 구분
	untracked: Staging Area에 비 업로드 된 파일 (새로운 파일)
	tracked: Staging Area에 업로드 되어있지만 변경 된 파일 (기존 파일의 변경점)

- 현제 상태 확인 명령어
```Shell
#defult: long (초보자는 기본형을 사용하는 것을 추천한다)
git status # 기본형

# short 
git status -s 
```


- Staging Area에 업로드 명령어
```Shell
# 단일 파일 추가
git add <파일이름.확장자>

# 특정(확장자) 파일만 추가
git add *.확장자

# 파일 전체 추가
git add *

# 해당 명령어 또한 전체 추가이다.
# 단 트래킹 한 파일을 rm 명령어로 삭제한 경우 
# git add * 명령어로는 삭제가 반영이 되지 않는다.
# 즉 아래 코드는 파일추가 + 갱신처리를 하는 코드이다.
git add . 
```

- 수정된 부분 확인하기
```Shell
# 기본 설정을 vscode 로 해 두었다면 vscode 로 편리하게 볼 수 있다.
# untracked tracked 파일의 변경점을 확인할 수 있다. 
git diff

# tracked 파일의 변경점을 확인할 수 있다
# untracked 된 파일은 포함하지 않는다.
git diff --staged

# 열지 않고 terminal 에서 파일내용을 확인하려면 아래 명령어를 사용하자.
cat c.txt
```

### Staging Area
- commit 을 위해선 파일들이 Staging Area 에 있어야 한다.  즉, Staging Area에 있는 파일만 commit 이 진행된다.

- 업로드한 파일 되돌리기
	 Staging Area에서 Working Directory로 되돌리고 싶다면 아래 명령어를 사용하자
	 staging area에서 delete, untracked 상태로 돌아간다.
``` Shell
git rm --cached <파일이름.확장자>

# 아래와 같은 방식으로도 사용 가능하다.
git rm --cached *.확장자 # .확장자를 가진 모든 파일 untracked
git rm --cached * # 모든 파일 untracked
```

### .Git Directory

- 여러가지 기능들을 만들어서 Staging Area에 업로드 해둔 것을 기반으로 commit 을 작성한다.
- 커밋을 완료하고 난 뒤 `git status`를 확인하면 untracked, tracked이 깔금하게 정리된 것을 알 수 있다.
```Shell
# 아무 옵션 없이 작성하면 vscode 상에서 기본적인 옵션이 나온다.
git commit 

# 메시지 바로 작성하기
git commit -m "작성하고싶은 내용"

# untracked 파일 까지 한거번에 커밋
git commit -am "작성하고싶은 내용"
```
	 commit 은 모듈(기능) 별로 분할하는 것이 좋다.
	 commit 은 타이틀에 맞게 주 목적에 맞게만 commit 해야한다. 
	 기본은 Staging Area에 있는 파일만 commit 된다.

- Check commit log 
```Shell
git log
```


## Third Step.

### How to make Branch
- 사용하는 이유는 원본을 수정하지 않으면서 내용을 추가할 수 있다.
- 수정한 내용을 원본과 합치기 편리하다.
- 원본과 변경점을 쉽게 알아볼 수 있다.

- branch 만들기
```Shell
git branch <branch name>
```

- branch list 확인
```Shell
git branch --list
```

- branch 접근
```Shell
git switch <branch name>
```

- branch coommit 를 그래프로 확인
```Shell
# (HEAD -> master)의 의미는 master branch 위치에 본인이 있다는 뜻이다.
git log --oneline --all --graph
```

- 분기가 나누어진 branch 를 master branch 로 병합하기
	 new branch -> master branch
```Shell
# 기준이 될 branch 로 이동
git switch mater

# 병합하기
git merge new branch

# 만약 브런치를 나누었지만 master branch 와 동일한 부분이 수정 되어있다면 충돌이 발생한다
# 해결방법 : 직접 코드를 수정해서 하나로 통합시킨다.
git add . # untracked tracked 갱신 후
git commit # commit 을 진행한다.
```



## Tips
- Git 명령어 단축하기
```Shell
git config --global alias.<사용자 설정명령어> <기존명령어>

# 내가 사용하는 short cut 예시
git config --global alias.a add
git config --global alias.c commit
git config --global alias.b branch
```
