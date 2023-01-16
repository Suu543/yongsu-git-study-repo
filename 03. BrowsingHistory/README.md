# Browsing History

contents:

1. Viewing the History
2. Filtering the History
3. Formatting the Log Output
4. Aliases
5. Viewing a Commit
6. Viewing the Changes Across Commits
7. Checking Out a Commit
8. Finding Bugs Using Bisect
9. Viewing the History of a File
10. Restoring a Deleting File
11. Finding the Author of Line Using Blame
12. Tagging
13. Browsing History Using VSCode
14. Exercise
15. Summary

## Starter

```txt
<!-- objectives.txt -->
OBJECTIVES

By the end of this course, you'll be able to
- Create snapshots
- Browse history
- Create and merge branches
- Collaborate with others
- Work with both the command line and visual tools
```

```txt
<!-- audience.txt  -->
AUDIENCE

This course is for anyone who wants to learn Git.
No prior experience is required.
```

```txt
<!-- toc.txt  -->
TABLE OF CONTENT

Creating Snapshots
  - Initializing a repository
  - Staging changes
```

```txt
<!-- sales-page.txt -->
```

```git
touch objectives.txt
// 상단의 objectives.txt 작성

git add objectives.txt
git commit -m "First: objectives text file for browsing history

// ----------------------------------------
touch audience.txt
// 상단의 audience.txt 작성

git add audience.txt
git commit -m "Second: audience text file for browsing history

// ----------------------------------------
touch toc.txt
// 상단의 toc.txt 작성

git add toc.txt
git commit -m "Third: toc text file for browsing history

// ----------------------------------------
sales-page.txt
// 상단의 sales-page.txt 작성

git add sales-page.txt
git commit -m "Fourth: sales-page text file for browsing history
```

## 1. Viewing the History

`commit(커밋)`한 내용을 살펴보고 싶을 때 `git log` 명령어를 사용할 수 있습니다.

```git
git log
```

`git log`는 `commit(커밋)` 생성 날짜, 저자, 내용, 고유값 모두를 확인할 수 있습니다. 경우에 따라 간략하게 전체 내용을 확인하고 싶을 때 다음 명령어를 사용할 수 있습니다.

```git
git log --oneline
```

`commit(커밋)` 내용을 간략하게 살펴보면서, 파일에 몇 번의 추가 및 삭제가 발생했는지 파악하고 싶을 때 다음 명령어를 사용할 수 있습니다.

```git
git log --oneline --stat
```

`commit(커밋)` 내용을 간략하게 살펴보면서, `commit(커밋)`간의 변경 사항을 확인하고 싶을 때 다음 명령어를 사용할 수 있습니다.

```git
git log --oneline --patch
git log --oneline -p
```

## 2. Filtering the History

테스트 목적으로 생성한 저장소에는 5 ~ 10개 정도의 `commit(커밋)`이 있습니다. 하지만 실무에서 여러 사람과 협업을 하는 경우, `commit(커밋)` 개수가 수백 수천 개가 될 수 있습니다.

이 경우 원하는 커밋에 접근할 때 `git log` 명령어만으로는 많은 시간이 소요됩니다. 이때 `git`에서 제공하는 필터링 기능을 통해 원하는 `commit(커밋)`을 빠르게 추출할 수 있습니다.

```git
// Last 3 commits
git log --oneline -3

git log --oneline --author="Mosh"

git log --oneline --after="2020-08-17"

git log --oneline --after="one week ago"

// 커밋 시 작성한 메시지에 GUI 단어를 포함하고 있는 commit, grep 커맨드는 대소문자 구분 방식으로 동작합니다..
git log --oneline --grep="GUI"

// 커밋 한 내용에 "OBJECTIVES"가 있는 경우
git log --oneline -S"OBJECTIVES"

// 커밋 한 내용에 hello()라는 글자가 있는 경우
git log --oneline -S"hello()"

// 커밋 한 내용에 "OBJECTIVES"가 있는 파일 변경 사항을 확인하고 싶을 때 --patch 사용
git log --oneline -S"OBJECTIVES" --patch

// commit의 범위(해시 값)를 이용해 필터링할 수 있습니다..
git log --oneline fb0d184..edb3594

// 특정 파일에 가해진 수정을 확인하고 싶은 경우 아래와 같이 작성할 수 있습니다.
git log --oneline toc.txt

// 실제 변경 사항을 확인하고 싶다면 아래와 같이 --patch를 붙이면 됩니다.
git log --oneline --patch -- toc.txt

// 단, 아래와 같이 --patch를 -- 뒤에 붙이면 파일명으로 간주하기 때문에 이 부분은 유의해야 합니다.
git log --oneline -- toc.txt --patch
```

## 3. Formatting the Log Output

로그를 작성할 때 앞에 함수 이름 혹은 키 값을 명시하는 것처럼, `commit(커밋)` 메시지를 직관적이게 출력하고 싶을 때 `--pretty` 속성을 사용할 수 있습니다.

- `%an`: 커밋 작성자 이름 (author)
- `%H`: 고유(해쉬) 값 (Full Hash)
- `%h`: 고유(해쉬) 값 축약형 (Abbreviated Commit Hash)
- `%cd`: 날짜 (Date)
- `%Cgreen`: 초록색 글자
- `%Cblue`: 파란색 글자
- `%Cred`: 빨간색 글자
- https://git-scm.com/docs/git-log

```git
git log --pretty=format:"hello"

// %an = author name
git log --pretty=format:"hello %an"

// %H = Full Hash
git log --pretty=format:"%an committed %H"

// %h = Abbreviated commit Hash
git log --pretty=format:"%an committed %h"

// %cd = date
git log --pretty=format:"%an committed %h on %cd"

// %Cgreen
git log --pretty=format:"%Cgreen%an committed %h on %cd"

git log --pretty=format:"%Cgreen%an %Creset committed %h on %cd"

// %Cred, %Cblue
git log --pretty=format:"%Cblue%an %Cgreen committed %h on %cd"
```

## 3. Aliases

자주 사용하는 포매팅에 이름을 붙여 간편하게 사용할 수 있습니다.

```git
// 자주 사용하는 포매팅에 이름을 붙여 등록할 수 있습니다.
git config --global alias.lg "log --pretty=format:'%an committed %h'"

// Alias 등록 여부를 확인합니다.
git config --global -e

git lg

git config --global alias.unstage "restore --staged ."

git config --global -e

git unstage
```

## 4. Viewing a Commit

`HEAD` 포인터를 이용해 커밋에 접근할 수 있습니다.

`HEAD`: 포인터로 현재 작업하고 있는 커밋(브랜치)이 어디인지 추적하는 역할을 합니다.

```git
// HEAD 포인터 기준 두 단계 이전의 커밋을 확인하고 싶은 경우
git show HEAD~2

// 특정 시점의 특정 파일을 확인하고 싶은 경우
git show HEAD~2:03.\ BrowsingHistory/workflow/objectives.txt

// 이름 혹은 상태를 확인하고 싶은 경우
git show HEAD~2 --name-only
git show HEAD~2 --name-status
```

## 5. Viewing the Changes Across Commits

`commit(커밋)`간의 변경 사항을 비교 확인하고 싶은 경우 명령어를 다음과 같이 작성할 수 있습니다.

```git
// 최신의 2개 커밋 사이의 차이를 확인하고 싶은 경우
git diff HEAD~2 HEAD

// 최신의 2개 커밋 사이의 특정 파일에서의 변경을 확인하고 싶은 경우
git diff HEAD~2 HEAD -- audience.txt

// 최신의 2개 커밋 사이의 파일명의 변경만 확인하고 싶은 경우
git diff HEAD~2 HEAD --name-only

// 최신의 2개 커밋 사이의 상태(m or n)만 확인하고 싶은 경우
git diff HEAD~2 HEAD --name-status
```

## 6. Checking Out a Commit

앞서 학습한 `log`는 원하는 시점의 `commit(커밋)`의 내용을 확인하는 목적으로 사용했습니다. 단순히 확인이 아닌 현재 `commit(커밋)` 위치를 추적하는 포인터 자체를 옮기고 싶을 때 `git checkout` 명령어를 사용할 수 있습니다. 간단하게는 특정 시점의 `snapshot(스냅샷)`에 접근하는 방식으로 이해할 수 있습니다.

<img src="https://cdn-images-1.medium.com/max/800/1*3fGisaVrHpF2iA8WPJpyOg.png" />

1. `commit(커밋)`은 다음 사진과 같이 전달받은 순서대로 쌓입니다.

- `master` 브렌치는 가장 최근에 업데이트된 `commit(커밋)`을 가리킵니다. `git` 에서는 이미 작성된 하나의 `commit(커밋)`을 `branch(브렌치)`라 칭합니다.

<img src="https://cdn-images-1.medium.com/max/800/1*wtWml3PdE05pHTzAsutRQQ.png" />

2. `HEAD`는 현재 작업 중인 브렌치를 추적하는 데 사용하는 포인터입니다.

- 사진을 보면 `HEAD` 포인터는 최신의 커밋을 가리키고 있는 것을 확인할 수 있습니다.

<img src="https://cdn-images-1.medium.com/max/800/1*vyuv_ZSj1USy-wB18Mb2sw.png" />

3. `checkout` 명령어를 사용하면 위 사진과 같이 `HEAD` 포인터의 위치를 변경할 수 있습니다.

```git
// FIRST 대신에 HASH 값을 통해 접근할 수 있습니다.
git checkout FIRST
```

<img src="https://cdn-images-1.medium.com/max/800/1*MZWeZb8fplNAww1-XyQn1A.png" />

4. `checkout` 명령어를 실행할 때 `detached HEAD` 오류가 발생합니다. 이는 말 그대로 가장 최신의 커밋인 `MASTER or MAIN`가 아닌 다른 곳을 가리키고 있고, 위 사진과 같은 오류가 발생하지 않도록 주의하라는 의미입니다.

만약 `FIRST` 브렌치를 확인만 하는 것이 아닌, `commit(커밋)`을 하면 해당 `commit(커밋)`은 위 사진과 같이 기존에 생성된 `commit(커밋)`과 어떠한 연관성이 없는 유령과 같은 역할로 남아있게 됩니다. 그러므로 `checkout` 명령어를 사용할 때는 그 목적이 뚜렷하지 않은 경우, 반드시 가장 최신의 `commit(커밋)`으로 되돌아와서 작업을 이어나가야 합니다.

```git
git log --oneline
// First Commit
git checkout 9472f20

// 가장 최신의 커밋
git checkout main
```

## 7. Finding Buts Using Bisect

팀으로 작업을 하다 보면 하루에도 수많은 커밋이 쌓이게 됩니다. 모든 `commit(커밋)`을 뒤져서 찾아낼 수도 있지만, 커밋 개수에 비례해 시간 소모도가 커집니다. 이 경우 `git bisect` 명령어를 사용하면 더욱 수월하게 문제를 해결할 수 있습니다.

- `git bisect`: 커밋의 특정 범위 내에서 이진 탐색을 통해 문제가 발생한 최초의 커밋을 찾는 데 도움을 주는 `git` 명령어입니다.

1. 문제가 발생한 `commit(커밋)`을 찾아 `Hash` 값을 기록합니다. `c167edf`
2. 문제가 발생하지 않은 `commit(커밋)`을 찾아 `Hash` 값을 기록합니다. `9472f20`

```git
// bisect를 활성화합니다.
git bisect start

// 문제가 발생한 커밋을 bad 속성과 함께 정의합니다.
git bisect bad c167edf

// 문제가 발생하지 않은 커밋을 good 속성과 함께 정의합니다.
git bisect good 9472f20

// HEAD 포인터 위치 확인
git log --oneline --all
```

이 단계까지 오면 `HEAD` 포인터가 `main or MASTER`가 아닌 다른 곳을 가리키는 것을 확인할 수 있습니다.

```git
Bisecting: 2 revisions left to test after this (roughly 2 steps)
```

위 결과 같은 `bad/good` 사이에 2개의 `commit(커밋)`이 있고, `bisect`를 2번만 더 수행하면 문제의 커밋을 찾을 수 있음을 의미합니다.

```git
git log --oneline --all
```

위 명령어 실행을 통해 `HEAD` 포인터 위치를 확인합니다. `HEAD` 포인터가 가리키고 있는 커밋에

4. 문제가 있다면(`HEAD` 포인터 기준 아래로 탐색을 시도합니다.): `git bisect bad`
5. 문제가 없다면(`HEAD` 포인터 기준 위로 탐색을 시도합니다.): `git bisect good`

- `4 ~ 5` 과정을 계속 수행하다 보면 버그를 발생시킨 최초의 커밋을 찾을 수 있습니다.

```git
git bisect good
git log --oneline --all

git bisect bad
git log --oneline --all
```

문제가 발생한 `commit(커밋)`을 찾았다면, 검토후 `HEAD` 포인터를 가장 최신의 커밋을 가리키도록 복구합니다.

```git
git bisect reset
```

## 8. Finding Contributors Using Shortlog

`commit(커밋)` 메시지를 간추려서 확인하고 싶을 때 `git shorlog` 명령어를 사용할 수 있습니다.

```git
git shortlog

git shortlog -n
git shortlog -n -s
git shortlog -n -s -e
```

## 9. Viewing the History of a File

한 파일에 발생한 변경 사항을 확인하고 싶을 때 다음과 명령어를 사용할 수 있습니다.

```git
git log toc.txt
git log --oneline toc.txt
git log --oneline --stat toc.txt
git log --oneline --patch toc.txt
```

## 10. Restoring Deleting File

작업 과정에 파일 삭제는 빈번히 발생하는 문제입니다. `git checkout` 명령어를 사용해 잘못 삭제한 파일을 복구해보겠습니다.

```git
// 현실에서는 잘못 삭제된 파일에 Remove toc.txt와 같은 커밋 메시지를 작성하지는 않습니다.
git rm toc.txt
git commit -m "Remove toc.txt"
// rm '03. BrowsingHistory/workflow/toc.txt'

git log --oneline toc.txt
// fatal: ambiguous argument 'toc.txt': unknown revision or path not in the working tree.

// 위 오류가 발생하면 다음과 같이 --를 추가하면 해결됩니다.
git log --oneline -- toc.txt

// 4cfb6c2 (HEAD -> main) Remove toc.txt
// ebb10b0 Third: toc text file for browsing history

// 이전 커밋(브렌치) ebb10b0에는 toc.txt 파일이 존재하기 때문에, 이전 시점으로 HEAD 포인터를 이동시켜 보겠습니다.
git checkout ebb10b0 toc.txt

// 이후 Working Directory 상태를 확인해보면 toc.txt 파일이 추가된 것을 확인할 수 있습니다.
git status -s
A toc.txt (A = Added)

// 다시 커밋을 해주면 잘못 삭제한 파일을 복구할 수 있습니다.
git commit -m "Restore toc.txt"
```

## 11. Finding the Author Line Using Blame

`git blame` 명령어는 특정 커밋을 식별할 때 사용합니다. 소스의 각 줄을 마지막으로 수정한 사람이 누구인지 그리고 어떤 커밋에서 변경사항이 적용되었는지 알려줍니다. 많이 사용하는 기능은 아니지만, 해당 소스가 어느 시점에 누가 왜 적용했는지 추적할 때 유용하게 사용할 수 있습니다.

```git
// audience.txt 마지막 수정 정보 조회
git blame audience.txt
// 이메일을 알고 싶은 경우
git blame -e audience.txt

// 1 ~ 3 줄의 마지막 수정 정보 조회
git blame -e -L 1,3 audience.txt
```

## 12. Tagging

웹 사이트를 이용할 때 북마크 기능을 사용하는 것 처럼, `git tag` 명령어를 사용해, `커밋(브렌치)`에 이름을 붙여 보다 더 논리적이고 체계적으로 파일을 관리할 수 있습니다.

```git
git log --oneline

// 4cfb6c2 (HEAD -> main) Remove toc.txt
// c167edf (origin/main, origin/HEAD) Fourth: sales-page text file for browsing history
//  ebb10b0 Third: toc text file for browsing history
//  5cb931b Second: audience text file for browsing history
//  c5be305 First: objectives text file for browsing history
//  7465fb8 YONGSU GIT COURSE Part2 Creating Snapshots
//  12887ed YONGSU GIT COURSE Part1
//  9472f20 Initial commit

git tag v1.0 12887ed
git log --oneline

// 4cfb6c2 (HEAD -> main) Remove toc.txt
// c167edf (origin/main, origin/HEAD) Fourth: sales-page text file for browsing history
//  ebb10b0 Third: toc text file for browsing history
//  5cb931b Second: audience text file for browsing history
//  c5be305 First: objectives text file for browsing history
//  7465fb8 YONGSU GIT COURSE Part2 Creating Snapshots
//  12887ed (tag: v1.0) YONGSU GIT COURSE Part1
//  9472f20 Initial commit

// 존재하는 태그 목록을 확인하고 싶은 경우
git tag

// 나중에 사용 할 태그를 만들고 싶은 경우
git tag -a v1.1 -m "My Version 1.1"

// 메시지를 따로 입력하지 않으면 커밋 메시지가 그 자리를 대체합니다.
// 메시지를 보고 싶은 경우 아래와 같이 작성합니다.
git tag -n

// 태그를 삭제하고 싶은 경우
git tag -d v1.1

git tag
```

## 13. Browsing History Using VSCode

- GitLens

## 14. Exercises

1. Make another commit. Now you should have two commits in your repo.
2. Show the changes in the last 2 commits.
3. Show all commits made by yourself. Use the one-liner option.
4. Show all commits with GUI in their message.
5. Show all commits with changes to file1.txt. Include the number of lines added/removed.
6. Compare the last two commits.
7. Check out the commit before the last commit. Note the detached HEAD in the terminal. Check out the master branch.
8. Show the author of every line in file1.txt.
9. Create a tag (v1.0) for the last commit. Show the history using the one-liner option and note the tag you just created.
10. Delete the tag.

```git
// 1. Make another commit. Now you should have two commits in your repo.
git add .
git commit -m "Update file1"

// 2. Show the changes in the last 2 commits.
git log --patch -2

// 3. Show all commits made by yourself. Use the one-liner option.
git log --author="Your name" --oneline

// 4. Show all commits with GUI in their message.
git log --grep="GUI"

// 5. Show all commits with changes to file1.txt. Include the number of lines added/removed.
git log --stat file1.txt

// 6. Compare the last two commits.
git diff HEAD~1 HEAD

// 7. Check out the commit before the last commit. Note the detached HEAD in the terminal. Check out the master branch.
git checkout HEAD~1
git checkout master

// 8. Show the author of every line in file1.txt.
git blame file1.txt

// 9. Create a tag (v1.0) for the last commit. Show the history using the one-liner option and note the tag you just created.
git tag v1.0
git log --oneline

// 10. Delete the tag.
git tag -d v1.0
```

## 15. Summary

```git
// Browsing History

// Viewing the history
git log --stat  # Shows the list of modified files
git log --patch # Shows the actual changes (patches)

// Filtering the history
git log -3  # Shows the last 3 entries
git log --author=“Mosh”
git log --before=“2020-08-17”
git log --after=“one week ago”
git log --grep=“GUI” # Commits with “GUI” in their message
git log -S“GUI” # Commits with “GUI” in their patches
git log hash1..hash2 # Range of commits
git log file.txt # Commits that touched file.txt

// Formatting the log output
git log --pretty=format:”%an committed %H”

// Creating an alias
git config --global alias.lg “log --oneline"

// Viewing a commit
git show HEAD~2
git show HEAD~2:file1.txt # Shows the version of file stored in this commit

// Comparing commits
git diff HEAD~2 HEAD # Shows the changes between two commits
git diff HEAD~2 HEAD file.txt # Changes to file.txt only

// Checking out a commit
git checkout dad47ed  # Checks out the given commit
git checkout master   # Checks out the master branch

// Finding a bad commit
git bisect start
git bisect bad # Marks the current commit as a bad commit
git bisect good ca49180 # Marks the given commit as a good commit
git bisect reset # Terminates the bisect session

// Finding contributors
git shortlog

// Viewing the history of a file
git log file.txt   # Shows the commits that touched file.txt
git log --stat file.txt  # Shows statistics (the number of changes) for file.txt
git log --patch file.txt  # Shows the patches (changes) applied to file.txt

// Finding the author of lines
git blame file.txt  # Shows the author of each line in file.txt

// Tagging
git tag v1.0 # Tags the last commit as v1.0
git tag v1.0 5e7a828 # Tags an earlier commit
git tag # Lists all the tags
git tag -d v1.0  # Deletes the given tag
```
