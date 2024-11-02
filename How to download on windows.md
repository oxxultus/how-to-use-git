## 사용하는 프로그램
> 기본적으로 `WIndow 11`부터 기본적으로 설치 되어있는 `Windows PowerShell` 을 사용한다.
> `Window 11` 이전 버전이라면 [Microsoft Store Window Terminal](https://www.microsoft.com/store/productId/9N0DX20HK701?ocid=pdpshare)에서 일단 다운 받으면 됩니다.
> 설치 시  이름은 `Windows Terminal` 이지만 설치되면 `Windows PowerShell`로 사용합니다.

- 기능
	1. 문자열 검색
	2. 탭으로 창 구분
	3. 화면 분할 기능
	4. 마우스 사용 가능(기존터미널은 마우스로 커서 위치조정 불가능)
	5. 터미널 테마 설정 가능, 여러가지 커스터마이징 허용

## How to install
- 기본적으로 Oh My Posh 라는 프로그램을 사용해 터미널 커스터 마이징을 사용할 예정이다.

### Step 1. Install Oh-My-Posh 
- `winget` 명령어를 사용해 설치하는 방식이다. (따라오기만 하면 빠르고 간단하다.)
- [Oh My Posh 공식 홈페이지](https://ohmyposh.dev/docs)를 확인하면 여러가지 설치방법이 존재한다.

1. Windows PowerShell 을 실행해서 다음
```PowerShell
winget install JanDeDobbeleer.OhMyPosh
```

- 다운로드 된 테마는 해당 위치에 저장된다.
- $HOME은 본인 admin폴더 위치이다.
- 테마 설정 시 사용해야 하므로 경로를 작성해 두는것을 추천합니다.
```PowerShell
C: $HOME\AppData\Local\Programs\oh-my-posh\themes
```
> 파일 폴더 내에서 AppData 폴더가 보이지 않는다면 아래 순서를 따라오세요
> 화면의 폴더 작업표시줄을  `보기` -> `표시`-> `숨긴항목` 체크 하면 나옵니다.

### Step 2. Setup Terminal Themes
> 테마를 설정하는 방법에 대해 작성되어 있습니다.

1. `Window PowerShell` 을 관리자 권한으로 실행합니다.
	- 오류가 있다면[Step 2. 1번에 대한 예외처리](#step-2-1번에-대한-예외처리) 으로 가자
```PowerShell
notepad notepad $PROFILE
```


2. 커맨드 입력
	1. [테마 종류 확인하기](https://ohmyposh.dev/docs/themes)에서 사용할 테마를 확인하고 온다.
	2. 본인은 **atomic.omp.json** 테마를 사용한다
	3. `C:$HOME \AppData\Local\Programs\oh-my-posh\themes`  이동하여 본인의 json파일 경로를 확인한다.
	4. 1번에서 `notepad notepad $PROFILE` 명령어를 작성하면 편집기가 열리게 된다.
	5. 해당 열린 메모장이나 편집기에 아래 내용을 작성하자
	6. 저장은 `ctrl + s` 로 저장하자
```text
oh-my-posh init pwsh --config '[로컬에 설치된 테마파일 경로]' | Invoke-Expression
```

	본인이 작성한 설정 정보
```text
oh-my-posh init pwsh --config 'C:\Users\admin\AppData\Local\Programs\oh-my-posh\themes\atomic.omp.json' | Invoke-Expression
```

4. 작성후 빨간 글씨로 스크립트 실행관련 오류가 뜬다면?
```PowerShell
Set-ExecutionPolicy RemoteSigned
```
	해당 코드를 실행하여 A를 입력하면 된다.

5. 실행확인 방법
	해당 명령어를 실행하면 테마를 바로 확인 가능하다.
	그냥 **재실행**을 추천한다
```PowerShell
Get-PoshThemes
```
	그냥 재실행 해도 된다. 재실행을 추천한다.

### Exception handling
#### Step 2. 1번에 대한 예외처리
	- 아무런 응답없음
	- **메모장**이나 **텍스트 편집기**가 열리지 않음
> 관리자 권한으로 실행된 `PowerShell` 에 해당 명령어를 작성하자.
```PowerShell
New-Item -Path $PROFILE -Type File -Force
```
	위 예외처리를 완료했다면 돌아가서 1번부터 다시 수행한다.
