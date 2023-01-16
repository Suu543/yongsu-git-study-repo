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

`commit(커밋)` 내용을 간략하게 살펴보면서, `commit(커밋)`간의 실제 변겅 사항을 확인하고 싶을 때 다음 명령어를 사용할 수 있습니다.

```git
git log --oneline --patch
git log --oneline -p
```

## 2. Filtering the History

테스트 목적으로 생성한 저장소에는 5 ~ 10개 정도의 `commit(커밋)`이 있습니다. 하지만 실무에서 여러 사람과 협업을 하는 경우, `commit(커밋)` 개수가 수백 수천 개가 될 수 있습니다.

이 경우 원하는 커밋에 접근할 때 `git log` 명령어만으로는 많은 시간이 소요됩니다. 이때 `git`에서 제공하는 필터링 기능을 통해 원하는 `commit(커밋)`을 빠르게 추출할 수 있습니다.

```git
// 최신 3개의 커밋
git log --oneline -3

// 명령어 입력 기준 전날 발생한 커밋
git log --oneline --after="yesterday"

// 명령어 입력 기준 한 주전 커밋
git log --after="one week ago"

// 작성자 이름을 기준
git log --oneline --author="cozyblank"


```
