# Snapshots

Contents:

1. Initializing a Repository
2. Git Workflow
3. Staging Files
4. Committing Changes
5. Skipping the Staging Area
6. Removing Files
7. Renaming or Moving Files
8. Ignoring Files
9. Short Status
10. Viewing Staged and Unstaged Changes
11. Viewing History
12. Viewing a Commit
13. Unstaging Files
14. Discarding Local Changes
15. Restoring a File to an Earlier Version
16. Creating Snapshots with other tools
17. Summary

## 1. Initializing a Repository

`Git` 학습에 사용할 저장소를 생성해 보겠습니다.

```bash
// 1. 폴더 생성

mkdir Moon

// 2. 생성한 Moon 폴더로 이동
cd Moon

// 3. 생성한 폴더에 git repository(저장소) 초기화 및 생성
git init

// 4. 생성한 git repository 확인
// 숨겨진 파일을 보고 싶은 경우 -a를 붙여줍니다.
ls -a

// 5. 생성한 git repository를 삭제하고 싶은 경우
rm -rf .git
```

## 2. Git Workflow

Git Workflow: `Git`이 동작하는 작업 절차 혹은 작업 흐름에 대해 알아보겠습니다.

<img src="https://cdn-images-1.medium.com/max/800/1*ZlTfgdLnXmsQ4UO06b184g.png" />

사진상의 디렉토리 색상별 의미

1. 보라색: 작업 폴더 (Local Directory)
2. 연초록색: 깃 리포지토리 (Git Repository - git init 통해 생성)

보라색 폴더에서 작업한다고 생각해보겠습니다. <br />
작업은 일반적으로 파일 추가, 삭제, 변경 등으로 구성됩니다. <br />

`Git Workflow`:
보라색 폴더에서 작업을 끝내고, `Git(깃)`의 데이터 단위인 `commit(커밋)`을 생성하고 이것을 `Git Repository(깃 리포지토리)`에 저장합니다.

깃 리포지토리에 커밋을 저장함에 한 공간을 더 거쳐 커밋을 처리합니다. 이 공간을 `Staging Area (임시 저장소)`라 부릅니다. 임시 저장소는 특정 지역의 물품을 모아 둔 배송 트럭으로 생각하면 쉽게 이해할 수 있습니다. 기능적, 의미론 적 한 단위인 파일을 모아 하나의 커밋을 생성하는 목적으로 사용하는 공간입니다.

`Staging Area` 기능:

1. `Git Repository`에 저장된 커밋(파일)과, 현재 `Staging Area`에 임시 저장된 커밋(파일) 비교해, 변경 사항을 알려줍니다.

- 변경 사항: 추가, 삭제, 갱신 등

커밋 생성과 저장 순서를 요약하면 다음과 같습니다.

```bash
Local Directory ==> Staging Area ==> Git Repository
```

`Git Workflow Summary`
<img src="https://cdn-images-1.medium.com/max/800/1*0XatSTFirkTcDXmkyXLLbw.png" />
<img src="https://cdn-images-1.medium.com/max/800/1*4KCmvE0nAUu2ZP5xjsBijg.png" />
<img src="https://cdn-images-1.medium.com/max/800/1*wkLdZoJnZNotEdU-gUMpWQ.png" />

1. 작업 폴더에서 작업을 완수합니다.

2. 작업이 끝난 파일을 `Staging Area`에 전달합니다.

3. `Staging Area`는 `Git Repository`에 저장된 파일과 추가된 파일에 어떤 차이점이 있는지 파악합니다. (검수 과정)

4. 검수가 끝나면 하나의 커밋 단위로 `Git Repository`에 전달합니다.

5. `Staging Area ==> Git Repository` 커밋 단계에, 내부적으로 커밋 하는 파일에 대한 `스냅샷(Snapshot)`을 생성합니다. 스냅샷은 새로운 파일이 `Staging Area`에 추가되었을 때 어떤 변경이 발생했는지 비교할 때 사용합니다.

6. 커밋 과정에 기록을 목적으로 커밋 메세지를 작성합니다.

- 메세지 포함 내용: ID, Message, Date/time, Author, Complete Snapshot

`Git Workflow In Detail`

<img src="https://cdn-images-1.medium.com/max/800/1*N3Vp-z6PzQP-RX-h8oEIgw.png" />
<img src="https://cdn-images-1.medium.com/max/800/1*v1IweT2ckF1VYcDlDzoz-w.png" />
<img src="https://cdn-images-1.medium.com/max/800/1*_vFV4nCp_6nzyZAN0hYqMA.png" />
<img src="https://cdn-images-1.medium.com/max/800/1*3a5iqJaRkygSPWZ8ed6TOg.png" />
<img src="https://cdn-images-1.medium.com/max/800/1*-7dOjMTOaSGyN-9WEg-r-w.png" />
<img src="https://cdn-images-1.medium.com/max/800/1*BewUAUYIM40JBl_kWvzvpw.png" />
<img src="https://cdn-images-1.medium.com/max/800/1*NX8tBvR_KPCm-OjZcnL0fA.png" />
<img src="https://cdn-images-1.medium.com/max/800/1*wyyrqgZlTqGlA1zQPQYfBA.png" />
<img src="https://cdn-images-1.medium.com/max/800/1*wr7nhXLqgvXlkN9PMpSS8A.png" />
<img src="https://cdn-images-1.medium.com/max/800/1*AI-cwWIwxn83bJwdWBps-w.png" />
<img src="https://cdn-images-1.medium.com/max/800/1*m8H4D6okz-9pyTmtY3SX-g.png" />
<img src="https://cdn-images-1.medium.com/max/800/1*aCTNqhCoIA87PtUQ0wtHrg.png" />

1. 빈 보라색 폴더에 `file1 and file2`가 추가됩니다.

2. `file1 and file2` 작업을 끝낸 후, `Staging Area`에 전달할 때 다음 명령어를 사용할 수 있습니다.

```bash
// add 명령어 다음에는 추가할 파일명을 작성합니다. 복수 개수일 때 띄어쓰기를 하고 작성하면 됩니다.
git add file1 file2

// 모든 파일을 Staging Area에 추가하고 싶은 경우 다음과 같이 명령어를 작성하면 됩니다.
git add .
```

3. `Staging Area`에 추가된 파일에 대한 검토가 끝났다면, `commit(커밋)` 명령어를 통해 `Git Repository`에 해당 파일을 저장할 수 있습니다.

- `commit` 명령어를 실행하면 `Staging Area`에 있는 파일에 대한 `스냅샷(Snapshot)`을 생성해 `Git Repository`에 전달하는 방식으로 동작합니다.

```bash
// 커밋 메시지를 작성하는 파일로 넘어가게 됩니다.
git commit

// 한 줄 커밋 메시지를 적고 싶은 경우
git commit -m "커밋 메세지"
```

4. `Git Repository`에 커밋된 파일은 전달된 순서대로 쌓이게 됩니다. 사진은 네 개의 커밋이 존재하기 때문에, 최초 커밋인 `Initial Commit`에 최하단에 자리 잡고 있습니다.

- 커밋이 순서대로 쌓이기 때문에, 특정 시점에 버그가 발생했다면 빠르게 그 시점으로 돌아가 수정 및 복원을 할 수 있다는 장점이 있습니다.

- 꼭 알아야 할 점은, 커밋 명령어가 실행되어도 `Staging Area`는 비워지지 않는다는 점입니다. `Staging Area`는 변경 사항 추적을 위해 `Git Repository`에 저장된 가장 커밋 `스냅샷(Snapshot)`을 유지하고 있습니다.

5. 보라색 작업 폴더에서 `file1`을 수정하고, 다음 명령어를 실행하면 변경된 사항이 `Staging Area`에 반영된다.

```bash
git add file1
```

6. `Staging Area`에서 변경 사항을 검토하고, `commit(커밋)`을 해주면 `Git Repository`에 변경 사항이 반영된 `스냅샷(Snapshot)`이 전달됩니다.

```bash
git commit -m "Fixed the bug in File1"
```

7. 보라색 작업 폴더에서 `file2`를 삭제했음에도, 여전히 `Staging Area`에는 `file2`가 남아 있습니다. 삭제했음을 `add and commit` 명령어를 통해 반영해야 최신의 상태를 유지할 수 있습니다.

```bash
git add file2
git commit -m "Removed Unused File2"
```

`Commit(커밋)`에는 작성한 커밋 메세지 뿐만 아니라, 세부 정보가 함께 저장됩니다. 여기서 주목할 세부 정보 중 하나는 `Commit ID (Unique Identifier)`입니다. 이는 커밋 고유 식별자로서 다른 매 커밋마다 다른 겹치지 않는 고유한 값이 할당됩니다.

내부적으로 이전 파일을 복원하거나 이전 시점으로 돌아갈 때, 고유한 값으로 `Commit ID`를 이용합니다.

## 3. Staging Files

이번에는 앞서 학습한 `Git Workflow`를 구현해보겠습니다.

```bash
// 1. 생성한 Moon 폴더에 파일 생성
echo hello > file1.txt
echo world > file2.txt

// 2. Staging Area 상태를 확인해보겠습니다.
git status

// Untracked File (빨간색): 아직 추적되지 않은 상태
// Tracked File (초록색): 추적되고 있는 상태

// 3. Untracked File ==> Tracked File
// 해당 폴더의 모든 파일을 추가하고 싶은 경우: git add .
// 모든 파일을 추가할 때 .env 파일 등 민감한 정보를 담고 있는 파일이 없는지 반드시 확인해야 합니다.
git add file1 file2

// 4. Staging Area 상태를 확인해보겠습니다.
git status

// 5. file1.txt 파일 내용을 변경해보겠습니다.
// >> 기호는 추가하기(이어붙이기) append를 의미합니다.
echo world >> file1.txt

// 6. Staging Area 상태를 확인해보겠습니다.
git status

// 7. file1.txt 변경 사항을 Staging Area에 반영해보겠습니다.
git add file1.txt

// 8. Staging Area ==> Git Repository
// 커밋 메세지가 한 줄인 경우
git commit -m ＂Commit File1 and File2＂

// 커밋 메세지가 여러 줄일 경우 (기본 에디터 확인)
git commit
```

<img src="https://cdn-images-1.medium.com/max/800/0*0PSqL72GPExLtoyf" />

## 4. Committing Best Practices

`Commit(커밋)` 명령어를 실행하는 기준은 다음과 같습니다.

<img src="https://cdn-images-1.medium.com/max/800/1*gdLDK5dQ7HwLrzV0viWy7Q.png" />

불필요한 `Commit(커밋)`은 다음과 같습니다.

1. 너무 잦은 커밋: Ex) 매 파일이 변경될 때마다 커밋
2. 너무 가끔 커밋: Ex) 수십 수백 개의 파일로 구성된 한 기능을 모두 완성 후 커밋

<img src="https://cdn-images-1.medium.com/max/800/1*eUrgluxZopWah24fqKLPBg.png" />
<img src="https://cdn-images-1.medium.com/max/800/1*V58HVOWKFXLKfJd9BjaUgg.png" />
<img src="https://cdn-images-1.medium.com/max/800/1*rWdHwiawg9ob7iTRz8FB9Q.png" />

반드시 피해야 할 `Commit(커밋)`:

- 두 개의 관련 없는 내용을 한 번에 커밋하는 것은 가능한 피해야 합니다. 이러면 커밋 메세지와 결과물 사이에 일관성이 없어 유지 보수 및 복원 시점을 잡기가 어려워 질 수 있습니다.

- 하나의 커밋에는 하나의 일관성 있는 주제를 담아야 합니다.

<img src="https://cdn-images-1.medium.com/max/800/1*slV1jzl292TrFcWcd9vDCQ.png" />
<img src="https://cdn-images-1.medium.com/max/800/1*_LSghPtOQHqvLDPUjqfYXg.png" />

Wording:

- Present: Fix the Bug
- Past: Fixed the Bug

## 5. Skipping the Staging Area

`Staging Area`를 건너뛰는 것이 가능합니다. 하지만 그 목적이 뚜렷한 경우에만 사용해야 합니다. 사실상 이 방식을 사용하는 경우는 없다 해도 무방합니다.

```bash
// 1. 파일 생성
echo test >> file1.txt

// 2. add 건너뛰고 바로 commit
git commit -a -m 'Fixed the bug that prevented the users from signing up'
git commit -am 'Fixed the bug that prevented the users from signing up'
```

## 6. Removing Files

`Commit(커밋)`한 파일을 삭제한 경우를 구현해보겠습니다.

```bash
// 1. file2.txt 삭제
rm file2.txt

// 2. Staging Area 상태를 확인해보겠습니다.
git status

// 3. Staging Area에 git add file2.txt를 하기 전 file2.txt 존재 여부를 확인해보겠습니다.
git ls-files

// file1.txt
// file2.txt

// 4. Staging Area에 변화 반영
git add file2.txt

// 5. 다시 확인해보기
// file2.txt가 삭제된 것을 확인할 수 있습니다.
git ls-files

// 6. Git Repository 반영하기
git commit -m "Remove Unused Code..."

// 위 과정을 한 번에 하고 싶은 경우
git rm file2.txt *.txt
```

## 7. Renaming or Moving Files

`Commit(커밋)`한 파일의 파일명 혹은 저장 위치를 변경한 경우를 구현해보겠습니다.

파일명만 변경했음에도, `git status` 명령어를 실행했을 때, 삭제된 파일로 간주하는 것을 확인할 수 있습니다. 이후 변경 사항을 `add` 명령어를 통해 `Staging Area`에 반영하면 정상적으로 `Renamed` 된 것을 파악하게 됩니다.

```bash
// 현재 폴더에 어떤 파일이 있는지 확인해보겠습니다.
ls

// 1. 파일 이름 변경하기
mv file1.txt main.js

// 2. git status 명령어를 통해 현재 상태 확인
git status

// deleted: file1.txt
// untracted files: main.js

// 3. Staging Area에 변경 사항 반영
git add file1.txt
git add main.js

// renamed: file1.txt ==> main.js

// 4. git status 명령어를 통해 현재 상태 확인
git status

// 5. Git Repository에 반영
git commit -m 'Rename file1.txt to main.js'
```

## 8. Ignoring Files

`.env` 파일과 같이 민감함 정보를 포함하고 있는 파일은 `Git Repository`에 반영하고 싶지 않은 상황이 생길 수 있습니다. 이때 `.gitignore` 파일을 생성하고 내부에 추적을 원치 않는 파일명을 작성하면, 추적하지 않습니다.

```bash
// 1. logs 폴더 생성
mkdir logs

// 2. logs 폴더에 파일 생성
echo hello > logs/dev.log

// 3. git status 명령어를 통해 현재 상태 확인
git status

// 4. .gitignore 파일 생성 (root)
echo logs/ > .gitignore

// 5. 기본 에디터를 이용해 파일을 확인해보겠습니다.
code .gitignore

// 6. git status 명령어를 통해 현재 상태 확인
git status

// Untracked Files: .gitignore

// 7. Staging Area에 변경 사항 반영
git add .gitignore

// 8. Git Repository에 반영
git commit -m "Add gitIgnore"
```

만약 `add` 명령어를 통해 `Staging Area`에 파일을 전달한 상태에서 `.gitignore`에 해당 파일을 추가하면, 해당 파일은 무시되지 않습니다.

```bash
// 1. bin 폴더 생성
mkdir bin

// 2. app.bin 파일 생성
echo hell > bin/app.bin

// 3. git status 명령어를 통해 현재 상태 확인
git status

// 4. Staging Area에 반영
git add .

// 5. Git Repository에 반영
git commit -m "Add app.bin file"

// 6. .gitignore 파일에 bin/ 폴더를 추가

// 7. Staging Area에 변경 사항 반영
git add .

// 8. Git Repository에 반영
git commit -m "Include bin/ in gitignore"

// 9. bin 폴더 무시 여부 검증을 위해, app.bin 파일 수정
echo helloworld > bin/app.bin

// 10. git status 명령어를 통해 현재 상태 확인
git status

// modified: bin/app.bin

// 11. 추적 여부 상세 검증
git ls-files

// .gitignore
// bin/app.bin
// file1.js
```

`bin` 폴더를 `gitignore` 파일에 추가했음에도 여전히 추적되는 것을 확인할 수 있습니다. 이 문제를 해결하는 두 가지 방법이 존재합니다.

1. 작업 폴더와 `Staging Area` 둘 다에서 파일을 삭제하는 방법

```bash
git rm file1.js
```

2. `Staging Area`에서만 파일을 삭제하는 방법

```bash
// 파일
git rm --cached file1.js

// 폴더
git rm -r --cached bin/
```

해결책을 적용해 보겠습니다.

```bash
// 1. Staging에서 추적한 bin 폴더 삭제
git rm -r --cached bin/

// 2. Git Repository에 반영
git ls-files
// .gitignore
// file1.js

// 3. git status 현재 상태 확인
git status

// deleted: bin/app.bin (commit 준비)

// 4. Git Repository에 반영
git commit -m 'Remove the bin directory that was accidentally committed...'

// 5. bin 폴더 추적 여부 검증
echo test > bin/app.bin

// 6. git status 현재 상태 확인
git status

// nothing to commit
```

- https://www.atlassian.com/git/tutorials/saving-changes/gitignore

## 9. Short Status

`git status` 명령어 실행 시 출력되는 현재 상태 값을 간략하게 만드는 방법을 알아보겠습니다.

```bash
// 1. 파일 두 개를 생성해 보겠습니다.
// file1.txt는 기존 내용에 새로운 내용 추가, file2.txt 파일 생성
echo sky >> file1.txt
echo fly > file2.txt

// 2. git status 명령어를 통해 현재 상태 확인
git status

// modified: file1.txt
// file2.txt

// 3. git status 요약 버전
git status -s

// M file1.txt - M (빨간색)
// ?? file2.txt

// 4. Staging Area에 변경 사항 반영
git add file1.txt

// 5. git status 요약 버전
git status -s

// M file1.txt - M (초록색)
// ?? file2.txt

// 6. file1.txt에 새로운 내용 추가
echo ocean >> file1.txt

// 7. git status 요약 버전
git status -s

// MM file1.txt
// ?? file2.txt

// 8. Staging Area에 변경 사항 반영
git add file1.txt

// M file1.txt
// ?? file2.txt

// 9. Staging Area에 변경 사항 반영
git add file2.txt

// M file1.txt
// A file2.txt
```

## 10. Viewing Staged and Unstaged Changes

`git diff` 명령어를 통해 `commit(커밋)` 하기 전 변경 사항을 간략히 확인할 수 있습니다.

1. `staged`된 파일 변경 사항을 비교하고 싶은 경우

```bash
git diff --staged
```

2. `unstaged`된 파일 변경 사항을 비교하고 싶은 경우

```bash
git diff (생략시 unstaged로 간주)
git diff --unstaged
```

```bash
// 1. file1.txt file2.txt 파일 생성
echo a > file1.txt
echo b > file2.txt

// 2. Staging Area에 변경 사항 반영
git add file1.txt file2.txt

// 3. Git Repository에 반영
git commit -m "file1 and file2"

// 4. file1.txt 텍스트 추가
echo text >> file1.txt

// 5. git diff 변경 사항 확인
git diff // or
git diff --unstaged

// 6. Staging Area에 변경 사항 반영
git add file1.txt

// 7. staged 된 파일의 변경 사항 확인
git diff --staged
```

<img src="https://cdn-images-1.medium.com/max/800/0*Leb_Pec_QWHOfOPi" />

Visual Diff Tools <br />
`git diff` 결과 값을 시각화해주는 도구가 몇 가지 있습니다.

## 11. Viewing History

`commit(커밋)` 한 내용을 확인하는 방법에 대해서 알아보겠습니다.

- 각 `commit(커밋)`에는 `고유값 (Unique Identifier)`이 할당됩니다. 이 값은 40글자로 구성됩니다 (Hexadecials).

```bash
// 1. 커밋한 내용을 최신순으로 출력합니다.
git log

// commit (40글자) (HEAD => master or main)
Author (저자)
Date (날짜)
Message (메세지)
```

`HEAD`는 현재 가리키고 있는 커밋 혹은 `branch(브랜치)`를 의미합니다. 기본값으로 가장 최근에 전달된 커밋 메시지를 가리키고 있습니다. `HEAD` 포인터를 이용해 이전 커밋으로의 돌아가 파일 수정 및 복원을 구현할 수 있습니다.

1. 커밋 메시지만 한 줄에 확인하고 싶은 경우

```bash
git log --oneline
```

2. 역순으로 커밋 메시지를 한 줄에 확인하고 싶은 경우

```bash
git log --oneline --reverse
```

## 12. Viewing a Commit

모든 `Commit(커밋)`을 나열하는 대신에, 특정 한 `Commit(커밋)` 만을 확인하고 싶은 경우 `git show` 명령어를 사용할 수 있습니다.

```bash
// 1. 한 줄에 커밋을 출력
git log --oneline

// 2. 50글자 중 7자리 숫자만 간략하게 출력됩니다. 이 중 자세하게 확인하고 싶은 커밋 값을 복사하고, `git show` 명령 뒤에 붙여주면 해당 커밋을 확인할 수 있습니다. Ex) c14c69b

git show c14c69b
```

1. 가장 최신의 `commit(커밋)`을 확인하고 싶은 경우

```bash
git show HEAD
```

2. `HEAD` 포인터를 이용해 이전 `commit(커밋)`에 접근하고 싶은 경우

```bash
// 최신 `commit(커밋)` 기준으로 2개 전 `commit(커밋)`을 확인할 수 있습니다.
git show HEAD~2
```

3. 특정 `commit(커밋)`의 특정 파일을 확인하고 싶은 경우

```bash
git show HEAD~2:.gitignore
```

4. `commit(커밋)`한 폴더의 모든 파일을 확인하고 싶은 경우

```bash
git ls-tree HEAD~1
```

<img src="https://cdn-images-1.medium.com/max/800/0*o7QzvhCOJnWgNZu2" />

`Git Objects`

- Commits
- Blobs (Files (파일))
- Trees (Directories (폴더))
- Tags (약어 (별명))

## 13. Unstaging Files

`git add` 명령어를 통해 `Staging Area` 업로드한 파일을 취소하고 싶을 때 `git restore` 명령어를 사용할 수 있습니다.

```bash
// 1. file1.txt and file2.txt 생성
echo a > file1.txt
echo b > file2.txt

// 2. Staging Area에 변경 사항 반영
git add .

// 3. Staging Area 반영을 취소하고 싶은 경우
git restore --staged file1.txt file2.txt

// 4. git status 현재 상태 확인
git status -s
```

`Staging Area`에 업로드한 모든 파일의 반영을 취소하고 싶은 경우

```bash
git restore --staged .
```

## 14. Discarding Local Changes

작업 폴더에서 작업 한 파일 중 `Staging Area` 업로드 하지 않은 모든 파일을 삭제하고 싶은 경우 `git clean` 명령어를 사용할 수 있습니다.

이 명령어는 사용 목적이 뚜렷하지 않으면 사용을 권장하지 않습니다.

명령어 옵션:

- `-f`: force(강제 삭제)
- `-d`: remove whole directories(모든 폴더 내용 및 폴더 삭제)
- `-h`: help (도움말)

```bash
git clean -h
git clean -fd
```

```bash
// 1. file1.txt and file2.txt 내용 추가
echo aaa file1.txt
echo bbb file2.txt

// 2. Staging Area에 변경 사항 반영
git add file.txt file2.txt

// 3. git restore 명령어로 Staging Area에 업로드한 내용 취소
git restore .

// 4. git status 현재 상태 확인
git status

// 5. git clean 명령어로 로컬 에서 작업한 모든 내용 삭제
git clean -fd

// 6. git status 현재 상태 확인
git status

// Nothing
```

## 15. Restoring a File to an Earlier Version

`Git`은 한 번 파일을 추적하기 시작하면, 이 파일의 모든 버전이 `Git` 내부 데이터베이스에 저장됩니다. 실수로 지우지 말아야 할 파일을 지우는 등 과거 기록을 통해 백업이 필요한 상황에 `HEAD` 포인터 and `git restore` 명령어를 조합해 사용할 수 있습니다.

```bash
// Tip: 1 ~ 2 과정을 한 줄에 하는 방법
git rm file1.txt

// 1. 이미 커밋한 이력이 있는 file1.js 삭제
rm file1.txt

// 2. Staging Area에 변경 사항 반영
git add file1.txt

// 3. Git Repository에 반영
git commit -m "Delete File1.txt"

// 4. 이 시점에 file1.txt를 지우면 안 됨을 파악
git log --oneline

// b50db6e (HEAD -> master) Delete File1.txt
// b5e4d66 thrid commit
// 23ecb88 second commit
f5098b1 initial commit

// 5. HEAD 포인트가 file1.txt 삭제를 반영한 커밋을 가리키고 있으므로, 이를 이전 커밋인 b5e4d66으로 옮기고 git restore 명령어를 사용

git restore --source=b5e4d66 file1.txt // or
git restore --source=HEAD~1 file1.txt

// 6. git status 현재 상태 확인
git status -s

// ?? file1.txt
```

## Summary

```bash
// Creating Snapshots

// Initializing a repository
git init

// Staging files
git add file1.js // stages a single file
git add file1.js file2.js // stages multiple files
git add *.js // stages with a pattern
git add . // stages the current directory and all its content

// Viewing the status
git status // full status
git status -s // short status

// Committing the staged files
git commit -m 'Message' // commits with an one-line message
git commit // open the default editor to type a long message

// Skipping the staging area (Not Recommended)
git commit -am "Message"

// Removing Files
git rm file1.js // removes from working directory and staging area
git rm --cached file1.js // removes from staging area only

// Renaming or moving files
git mv file1.js file1.txt

// Viewing the staged/unstaged changes
git diff // shows unstaged changes
git diff --staged // shows staged changes
git diff --cached // same as the above

// Viewing the history
git log // full history
git log --oneline // summary
git log --reverse // lists the commits from the oldest to the newest

// Viewing a commit
git show 82la2ff // shows the given commit
git show HEAD // shows the last commit
git show HEAD~2 // Two Steps before the last commit
git show HEAD:file.js // shows the version of file.js stored in the last commit

// Unstaging files (undoing git add)
git restore --staged file.js // copies the last version of file.js from repo to index

// Discarding local changes
git restore file.js // copies file.js from index to woking directory
git restore file1.js file2.js // restore multiple files in wokring directory
git restore . // discards all local changes (except untracked files)
git clean -fd // removes all untracked files

// Restoring an earlier version of a file
git restore --source=HEAD~2 file.js
```
