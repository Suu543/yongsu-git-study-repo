# Git

1. What is Version Control System?
2. What is Git?
3. Installing Git
4. Configuring Git

## 1. What is Version Control System?

`Git`을 이해하기 앞서 `VCS(버전관리 시스템: Version Control System)`이 무엇인지 알아보겠습니다.

`VCS(버전관리 시스템: Version Control System)`이란 파일 변화를 시간에 따라 기록하고, 필요에 따라 특정 시점의 버전을 다시 불러올 수 있는 시스템을 의미합니다.

`VCS`를 사용하면 잘못 수정 혹은 삭제된 파일을 이전 상태로 되돌릴 수 있고, 변경 사항 비교 및 변경 시기 추적을 쉽게 할 수 있습니다.

`VCS`는 크게 세 종류로 구성됩니다.

1. Local VCS(로컬 버전관리 시스템: Local Version Control System)
2. CVCS(중앙집중식 버전관리 시스템: Centralized Version Control System)
3. DVCS(분산 버전관리 시스템: Distributed Version Control System)

### Local Version Control System

<img src="https://cdn-images-1.medium.com/max/800/1*d9M_MBivGkJIf8lqVUlQ5w.png" />

`Local VCS(로컬 버전관리 시스템)`은 데이터베이스를 통해 디렉토리(폴더) 버전 관리의 단점을 보완했습니다. 하지만 개인 컴퓨터에서만 디렉토리에 접근할 수 있기 때문에, 다른 개발자와의 협업이 필요한 작업에는 적합하지 않다는 단점이 있습니다.

### Centralized Version Control System

<img src="https://cdn-images-1.medium.com/max/800/1*SDj9TdcYCPGuH7ZcB6SJbg.png" />

`CVCS(중앙집중식 버전관리 시스템)`은 다른 개발자와의 협업 과정에 생기는 문제를 해결하기 위해 개발되었습니다. 이 방식은 파일을 관리하는 서버를 별도로 두고, 클라이언트가 중앙 서버에서 파일을 받는 방식으로 동작합니다.

하지만 중앙 서버에 문제가 발생한 경우, 어떠한 작업도 수행할 수 없다는 치명적 단점이 존재합니다. 또한 중앙데이터베이스가 있는 하드디스크에 문제가 생길 경우 그간 작업해온 프로젝트의 모든 기록을 잃을 수 있다는 위험이 존재합니다.

### Distributed Version Control System

<img src="https://cdn-images-1.medium.com/max/800/1*KJ7hP_B3MZOHyqXLOWxs6g.png" />

`CVCS(중앙집중형 버전관리 시스템)`의 저장소가 중앙 서버에 있는 것과 달리 `DVCS(분산 버전관리 시스템)`은 모든 클라이언트가 저장소가 될 수 있습니다.

분산 버전관리 시스템은 최신의 파일 혹은 폴더를 복사하는 것이 아닌, 저장소 전체를 복사하는 방식으로 동작합니다. 이 때문에 서버에 문제가 생기더라도 이 복제물로 작업을 이어갈 수 있고, 클라이언트 간의 진행 상태를 비교할 수 있고, 서버에 문제가 생기더라도 클라이언트 중 한 명을 골라 서버를 복원할 수 있습니다. 이러한 확장성과 복제성의 특징 때문에 버전 관리 시스템 중 협업에 가장 많이 사용되는 방식입니다.

## 2. What is Git?

`Git`은 가장 유명한 `DVCS 분산 버전관리 시스템(Version Control System)` 중 하나 입니다.

`Git`의 특징은 다음과 같습니다.

- `Git`은 소스코드 교환 없이 같은 파일을 여러 명이 작업하는 병렬 개발이 가능하며, 버전 관리가 쉽습니다. (Branch and Merge)
- `Git`은 커밋 단위로 파일을 관리하기 때문에, 원하는 커밋 시점으로 되돌아갈 수 있습니다(Checkout).
- `Git`은 분산 버전 관리 시스템으로 동작하기 때문에 로컬에서 개발할 수 있으며, 중앙 저장소에 문제가 생겨도 복원이 쉽습니다.
- `Git`을 통해 버전 관리, 패치 및 배포를 체계적으로 할 수 있습니다.

### Git Snapshot

`Snapshot(스냅샷)`은 특정 시간에 데이터 저장 장치의 상태를 별도의 파일이나 이미지로 저장하는 기술로, 스냅샷 기능을 이용하며 데이터를 저장하면 유실된 데이터 복원과 일정 시점의 상태로 데이터를 복원할 수 있습니다.

깃은 다른 버전 관리 도구와 달리 `Snapshot(스냅샷)` 방식을 이용합니다. 파일을 복사하는 방식으로 수정본을 관리하면 같은 내용을 반복해서 저장하기에 많은 용량을 차지합니다. 또 수정된 부분을 일일이 찾아야 하므로 검색할 때도 많은 시간이 소요됩니다. 이러한 시스템적인 단점을 해결하고자 변경된 파일 전체를 저장하지 않고, 파일에서 변경된 부분을 찾아 수정된 내용만 저장합니다. 마치 변화된 부분만 찾아 사진을 찍는 것과 같다고 하여 `Snapshot(스냅샷)` 방식이라고 합니다.

### Git Repository

`저장소(Repository)`는 파일이 저장되는 저장소를 의미합니다. 두 종류의 저장소가 존재합니다.

1. `Local Repository(로컬 저장소)`
2. `Remote Repository(원격 저장소 = 중앙 저장소)`

저장소를 불러오는 절차는 다음과 같습니다.

1. `Remote Repository(원격 저장소)`를 불러옵니다 (Clone).
2. 커밋을 통해 `Local Repository(로컬 저장소)`에 업데이트된 파일을 저장합니다.
3. 푸시를 통해 `Local Repository` 내용을 `Remote Repository`에 반영합니다 (Push).

### Git Areas

<img src="https://cdn-images-1.medium.com/max/800/0*TCb3Yl4W6XoBMLtZ" />
<img src="https://cdn-images-1.medium.com/max/800/0*T-2tdm98RT7DXF3E.png" />

Working Area (Working Directory):

- 현재 작업 중인 디렉토리(폴더)를 의미합니다.

Staging Area (Index):

- `Working Area(Directory)`에 추가된 파일이 임시로 저장되는 영역입니다. 이 위치에서 파일을 선별해 `Local Repository`에 저장할 수 있습니다.

Repository Area (Commit Area):

- `Staging Area`에서 커밋된 파일들이 저장되는 저장소입니다. 파일 수정사항에 대한 `스냅샷(Snapshot)`을 가지고 있습니다. `Push`를 통해 `Remote Repository`에 저장할 수 있습니다.

### Git Basic Features

1. Add(에드)

- `Working Area(Directory)`에서 작업한 내용을 `Staging Area (Index)`에 추가해줍니다.
- `Working Area(Directory)` ==> `Staging Area (Index)`

2. Commit(커밋)

- `commit(커밋)`은 `Git`이 파일을 관리하는 단위입니다.
- `Staging Area`에 추가된 내용을 `Local Repository`에 저장해줍니다.
- `commit(커밋)`에는 날짜, 시간, 제목, 내용 등을 같이 메모로 남길 수 있습니다.
- `Staging Area (Index)` ==> `Local Repository`

3. Push(푸쉬)

- `Local Repository`에 업데이트한 내용을 `Remote Repository`에 반영하는 과정입니다.
- `Local Repository` ==> `Remote Repository`

4. Pull(풀)

- `Push`와는 반대로 `Remote Repository`에 있는 내용을 `Local Repository`에 반영하는 과정입니다.
- `Pull(풀)`을 이용해 다른 사람이 `Push`한 내용을 `Local Repository`에 반영해 작업을 이어갈 수 있습니다.
- `Remote Repository` ==> `Local Repository`

5. Tag(태그)

- `commit(커밋)`은 수십 자리의 숫자 및 영문자 조합으로 이루어진 해쉬값이기 때문에, 이 값에 이름을 붙여 보다 쉽게 `commit(커밋)`에 접근할 수 있게 해줍니다.
- `Tag` = `commit(커밋)` 별명

6. `Branch(브랜치)`

<img src="https://cdn-images-1.medium.com/max/800/0*JoKbkNE-CbgYYA9x" />

- `commit(커밋)`을 기준으로 구분된 파일을 분기로 나누어 새로운 커밋을 가지(분기)를 `branch(브랜치)`라고 합니다.

7. Checkout(체크아웃)
   <img src="https://cdn-images-1.medium.com/max/800/0*sIm0lqh7YR9U466m" />

- `Git`은 커밋 단위로 파일을 관리하기 때문에, 원하는 커밋 시점으로 되돌아갈 수 있습니다.
- 원하는 커밋 시점으로 되돌아가기 = `checkout(체크아웃`
- `checkout(체크아웃)`을 이용해 `branch(브랜치)` 생성, 삭제 및 수정 등 다양한 작업을 할 수 있습니다.

### Summary

`Git`은 분산 버전 관리 시스템으로써 다음과 같은 이점을 제공합니다.

1. 파일 버전을 쉽게 관리할 수 있게 해줍니다.
2. 병렬 개발을 통해 다른 사람과 쉽게 협업할 수 있습니다.
3. 분산 버전 관리 시스템으로 동작하기 때문에 로컬에서 개발할 수 있으며, 중앙 저장소에 문제가 생겨도 복원이 쉽습니다.

## 3. Installing Git
git: https://git-scm.com/
git-bash: 


## 4. Configuring Git

`git` 초기 설정에 대해 알아보겠습니다.

1. `Git Bash`를 실행합니다.
2. 아래 명령어를 입력합니다.

```cmd
git config --global user.name "본인이름"
git config --global user.email "본인 이메일 주소"

// default editor - I'm going to use Visual Studio Code in this course
// --wait flag tells the terminal window to wait until we close the new VSCode Instance
git config --global core.editor "code --wait"

// Default Editor
git config --global -e

git config --global core.autocrlf input

// 제대로 입력되었는지 확인을 위해 다음 명령어를 입력할 수 있습니다.
git config --list

```

<img src="https://cdn-images-1.medium.com/max/800/0*GA8kb4dUgV7s2gii" >

### 소스 포맷 및 공백

`Git`을 이용해 협업할 때 소스 포맷(Formatting)과 공백 문제가 자주 발생합니다. `Git`에는 해당 문제 해결을 도와주는 몇 가지 설정이 있습니다.

- `Linux(유닉스 계열)`
  - 리눅스에서는 줄 바꿈 `LF`가 기본값입니다. `(\n)`
- `Windows`
  - `Windows`에서는 줄 바꿈을 `CRLF`가 기본값입니다. `(\r\n)`

1. core.autocrlf

- 윈도우 운영 체제에서 개발하는 사람과 협업하는 경우 `줄 바꿈(New Line)` 문자에 문제가 발생합니다.
- 윈도우 운영 cp체에서 줄 바꿈 문자로 `CR(Carriage-Return)`과 `LF(Line Feed)` 문자를 둘 다 사용합니다.
- 맥과 리눅스 운영체제는 윈도우와 달리 줄 바꿈 문자로 `LF(Line Feed)` 문자만 사용합니다.

`Git`은 커밋할 때 자동으로 `CRLF`를 `LF`로 변환해주고 반대로 `Checkout`을 할 때 `LF`를 `CRLF`로 변환해주는 기능이 있습니다.

`core.autocrlf` 설정으로 이 기능을 켤 수 있습니다. 윈도우 운영 체제에서 이 값을 `true`로 설정하면 `checkout`할 때 `LF` 문자가 `CRLF` 문자로 변환됩니다.

```cmd
$ git config --global core.autocrlf true // window
```

줄 바꿈 문자로 `LF`를 사용하는 `Linux` and `MacOS`는 `checkout`할 때 `Git`이 `LF`를 `CRLF`로 변환할 필요가 없습니다. 또한 우연히 `CRLF`가 포함된 파일이 저장소에 있어도 `Git`이 알아서 고쳐주면 좋을 것입니다. `core.autocrlf` 값을 `input` 값으로 설정하면 커밋지 `CRLF`를 `LF`로 변환해줍니다.

```cmd
$ git config --global core.autocrlf input
```

이 설정을 사용하면 윈도우 운영 체제에서는 `CRLF`를 사용하고, `Linux` and `MacOS` 저장소에서는 `LF`를 사용할 수 있습니다. 윈도우 운영 체제에서만 개발한다면 이 기능이 필요 없으므로 다음과 같이 `false`로 설정하면 이 기능이 꺼지고 `CR` 문자 또한 저장소에 저장되게 됩니다.

```cmd
$ git config --global core.autocrlf false
```
