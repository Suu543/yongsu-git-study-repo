# Branching

<img style="width: 100vw" src="https://cdn-images-1.medium.com/max/800/1*nRxq_WLgPL8Y9RMuGUNOZg.png" />

contents:

1. What are Branches?
2. Working with Branches
3. Comparing Branches
4. Stashing
5. Merging
6. Fast-forward Merges
7. Three-way Merge
8. Viewing Merged and Unmerged Branches
9. Merge Conflicts
10. Merge Tools
11. Aborting a Merge
12. Undoing a Faulty Merge
13. Squash Merging
14. Rebasing
15. Cherry Picking
16. Picking a File from Another Branch
17. Branching in VSCode

## 1. What are Branches?

<img style="width: 100vw" src="https://cdn-images-1.medium.com/max/800/1*xJI1xHbnZNN7I-q7N1y7QA.jpeg" />

소프트웨어를 개발하다 보면 그 규모가 커졌을 때 협업이 필요한 순간이 있습니다.
협업 방식은 대게 다음 순서로 진행됩니다.

1. 서비스에 필요한 기능 세분화
2. 기능별로 팀 조직
3. 각 팀이 개발한 기능을 하나로 병합해 소프트웨어 배포

모든 팀이 같은 `저장소(Repository)`를 사용함과 동시에, 팀별로 코드를 관리하고 개발에 사용할 독립적 영역이 필요합니다. <br />

`Git`에서는 이러한 독립적인 영역을 `브랜치(branch)`라고 칭합니다.

`브랜치(branch)`는 나무에 뻗어난 가지를 의미합니다. 나무 한 그루에는 수많은 가지가 제각기 다른 방향을 바라보고 있지만, 모든 나뭇가지는 같은 뿌리를 공유하고 있습니다.`Git`에서 사용하는 `브랜치(branch)` 또한 나무의 나뭇가지와 똑같이 동작합니다. 각자 방향으로 뻗어 나가 꽃을 피우지만, 이 모든 가지가 합쳐져 하나의 나무를 이루게됩니다.

이해를 돕고자 상단에 있는 문어 캐릭터를 생각해보겠습니다.
세 명의 사람이 하나의 소프트웨어를 작업한다고 했을 때

- A (벌거벗은 문어): 소프트웨어 배포에 사용할 `브랜치(branch)`입니다.
- B (선글라스를 착용한 문어): 벌거벗은 문어(A)를 기준으로 선글라스 기능을 담당하는 팀입니다.
- C (카우보이모자를 착용한 문어): 벌거벗은 문어(A)를 기준으로 카우보이 모자 착용 기능을 담당하는 팀입니다.

`B와 C 브랜치(branch)`에서 기능 구현을 끝내고, <br />
`A` 브랜치에 두 브랜치를 병합하면 최종적으로 선글라스와 카우보이모자를 착용한 문어를 구현할 수 있습니다.

`브랜치(branch)` 생성 시점은 크게 두 종류로 분류할 수 있습니다.

1. 소프트웨어 개발 시작과 함께 생성 (벌거벗은 문어 예시)
2. 소프트웨어 개발 도중 생성

소프트웨어 개발 도중에 생성하는 경우를 알아보겠습니다.

다음 사진을 보면 `MASTER` 이름의 `브랜치(branch)`가 하나 존재합니다. <br />
해당 `브랜치(branch)`는 현재 4개의 커밋을 한 상태입니다.

<img style="width: 100vw" src="https://cdn-images-1.medium.com/max/800/0*jZ3eUplujpYbJ9Y9" />

`MASTER Branch` 작업 도중 기능 개발팀이 결성되어, 해당 팀이 작업에 사용하는 `Feature Branch`를 하나 생성했습니다. 해당 `브랜치(branch)`는 소트프웨어 개발 시작과 함께 생성된 것이 아니므로, 기존에 `Master Branch`에서 작업한(4개의 커밋) 내용을 기준으로 작업을 진행합니다. <br />

이를 시각화 하면 다음과 같이, `Feature Branch`가 `MASTER Branch` `FEATURE`가 마지막으로 작업한 곳을 가리키고 있습니다.

<img style="width: 100vw" src="https://cdn-images-1.medium.com/max/800/1*CmQO54FZFFToqC3R0A73Ng.png" />

`Feature Branch`를 생성 후 작업을 이어나가면 다음 사진과 같은 형태를 띄게 됩니다. 현재 사진을 통해 `Feature` 팀이 두 개의 커밋을 생성한 것을 확인할 수 있습니다.

<img style="width: 100vw" src="https://cdn-images-1.medium.com/max/800/0*PlsQZZ1hx9BJRvRB" />
<img style="width: 100vw" src="https://cdn-images-1.medium.com/max/800/0*9QSKNilXwnLncWK1" />

여러 종류의 `브랜치(Branch)`가 존재할 때, 어느 `브랜치(Branch)`에서 작업하고 있는지 확인할 수단이 필요합니다. `Git`에서는 `HEAD Pointer(포인터)`를 통해 현재 작업하고 있는 `브랜치(Branch)`를 확인할 수 있습니다. 다음 사진을 보면 현재 `HEAD Pointer`는 `Master Branch`를 가리키고 있습니다.

<img style="width: 100vw" src="https://cdn-images-1.medium.com/max/800/0*gfOWF2lM4B8YFAz5" />

이후 학습할 `git checkout` 명령어를 통해 다음 사진과 같이 `HEAD Pointer`가 `Feature Branch`를 가리키도록 만들 수 있습니다.

<img style="width: 100vw" src="https://cdn-images-1.medium.com/max/800/0*j8vSuW5eWg33f8yy" />

`HEAD Pointer`의 위치 변경은 대게 다른 브랜치에서 작업한 내용을 `Master Branch`에 병합할 목적으로 사용합니다. <br />

---

학습하기에 앞서 한가지 기억해야 할 점은, 최종적으로 모든 브랜치에서 작업한 내용은 `Master Branch`에 병합된다는 점입니다.

## 2. Working with Branches

`브랜치(Branch)`를 생성하는 방법에 대해 알아보겠습니다.

```git
// 1. bugfix 브랜치 생성
git branch bugfix

// 2. 현재 존재하는 브랜치 확인
git branch

// 3. 현재 사용 중인 브랜치 확인 (HEAD Pointer가 가리키는 곳)
git status

// 4. 작업 브랜치를 변경하고 싶은 경우
git switch bugfix

// 5. 이미 생성된 브랜치 이름을 변경하고 싶은 경우
git branch -m bugfix bugfix/signup-for

// 6. audience.txt 파일 수정
/*
// 수정 전
AUDIENCE

This course is for anyone who wants to learn Git.
No prior experience is required.
*/

/*
// 수정 후
AUDIENCE

This course is for anyone who wants to learn Git.
WHO THIS COURSE IS FOR (수정 내용)
*/

// 7. 수정 사항 확인 (Local Repository)
git status

// 8. 수정 사항 Staging Area에 반영
git add .

// 9. Staging Area에서 검토 후 Commit Repository에 반영
git commit -m "Fix the bug that prevented the users from signing up"

// 10. 작업 브랜치 커밋 내용 검토
git log --oneline

// 11. 작업 브랜치를 Master 브랜치로 변경
git switch master

// 12. audience.txt 파일 검사 시, bugfix 브랜치에서 수정한 내용이 반영되지 않은 것을 확인할 수 있습니다.
code audience.txt

// 13. 작업 중인 브랜치 뿐만 아니라 모든 브랜치의 내용을 확인하고 싶은 경우 --all 속성을 추가할 수 있습니다.
git log --oneline --all

// 14. 브랜치를 삭제하고 싶은 경우 -d 속성을 사용할 수 있습니다. 하지만, Master Branch에 bugfix 브랜치에서 변경한 내용을 병합하지 않은 상태에서 삭제 시 오류를 출력합니다.
git branch -d bugfix/signup-for
// error: The branch 'bugfix/signup-form' is not fully merged.


// 15. Master 브랜치에 병합 전임에도 강제 삭제를 원하는 경우 -D 속성을 사용할 수 있습니다.
git branch -D bugfix/signup-for

// 16. 브랜치 생성과, 해당 브랜치로의 전환을 한 번에 하고 싶은 경우: branch + switch
git switch -C bugfix/login-form
```

## 3. Comparing Branches

작업한 브랜치를 `Master or Main` 브랜치에 병합하기 전 변경 사항을 확인해야 합니다. <br /> `git diff` 명령어를 통해 브랜치간 변경 사항을 검토할 수 있습니다.

```git
// 1. Master or Main 브랜치와 bugfix/signup-form 브랜치 사이의 커밋 비교
git log master...bugfix/signup-form

// 2. Master or Main 브랜치와 bugfix/signup-form 사이에 변경된 파일 검토가 필요한 경우
git diff master...bugfix/signup-form

// 3. 브랜치 사이의 변경된 파일 이름만 검토하고 싶은 경우
git diff --name-only master...bugfix/signup-form
git diff --name-status master...bugfix/signup-form
```

## 4. Stashing

<img src="https://cdn-images-1.medium.com/max/800/0*T-2tdm98RT7DXF3E.png" />

다음 사진을 보면 좌측 끝에 `Stash (Temporary Storage)`가 존재합니다. <br />

`branch(브랜치)`를 변경할 때, 기본적으로 `Staging Area`가 초기화됩니다. `Local Change`를 그대로 유지하고 싶은 경우가 존재합니다. 이때 `임시 저장소(Stash)`를 사용하면 문제를 효과적으로 해결할 수 있습니다.

A 브랜치에서 B 브랜치로 전환하는 과정에, B 브랜치에서 작업하기 전 A 브랜치 로컬에서 변경한 내용을 검토하고, 이를 참고해 작업해야 할 경우, `임시 저장소(Stash)`를 통해 A 브랜치 내용을 검토하고 작업을 이어나갈 수 있습니다.

Ex) 동시 다발적으로 해야 할 일들이 생기면, 일의 우선순위가 계속해서 바뀌게 됩니다. 예를 들면, 항목 정렬에 관한 작업을 하는 중 급하게 다른 버그를 처리하는 등 우선순위가 먼저인 일을 끝내야 할 상황이 있습니다. 이때 우선순위가 높은 일에 해당하는 `branch(브랜치)`를 생성해야 하는 데, 다른 브랜치로 전환하려면 반드시 작업 중인 모든 내용을 커밋 하거나 혹은 `로컬 폴더(Working Directory)`를 비워야 합니다. 하지만 마무리되지 않은 작업을 커밋 할 수는 없으므로 `임시 저장소(Stash)`를 이용해 임시 보관을 하고, 우선순위가 높은 일을 끝내고 이후 다시 `임시 저장소(Stash)`에 저장한 파일을 불러와, 이어서 작업하는 용도로 `stash`를 사용할 수 있습니다.

`임시 저장소(Stash)`를 생성해 보겠습니다.

```git
code audience.txt
/*
AUDIENCE

This course is for anyone who wants to learn Git.
No prior experience is required.
*/

/* audience.txt 파일을 다음 내용으로 변경하겠습니다.
* AUDIENCE

This course is for anyone who wants to learn Git.
No prior experience is required.
*/
```

로컬에서 변경이 발생했지만, 아직 커밋을 하지 않은 상태입니다.

```git
git switch bugfix/signup-form
```

`Git`은 브랜치 변경 시, 작업 중인 로컬 폴더를 초기화해야 예상치 못한 오류를 방지할 수 있습니다. <br />

로컬 폴더를 초기화 하는 과정에 커밋하지 않은 내용을 `임시 저장소(Stash)`를 이용해 저장할 수 있습니다.

```git
// audience.txt 파일 변경 사항이 stash에 저장됩니다.
git stash push -m "First Stash - audience.txt"

// 생성한 newfile.txt는 stash에 저장되지 않습니다.
echo hello > newfile.txt

// newfile.txt를 stash에 저장해보겠습니다.
git stash push -m "Second Stash - newfile.txt

// 저장된 모든 stash를 검토해보겠습니다.
git stash list

/*
stash@{0}: On main: First Stash - audience.txt
stash@{1}: On main: Second Stash - newfile.txt
*/
```

로컬에서 작업한 내용을 모두 `임시 저장소(Stash)`에 저장했습니다. <br />
작업 중인 `로컬 폴더(Working Directory)`가 비워졌기 때문에, 브랜치 변경이 가능합니다.

```git
// Working Directory(Area)는 비워진 상태입니다.
// 예상치 못한 오류 없이 브랜치 변경이 가능합니다.
git switch bugfix/signup-form

// 다시 master or main 브랜치로 변경해보겠습니다.
git switch master

// 저장된 stash를 검토해보겠습니다.
git stash list

/*
stash@{0}: On main: First Stash - audience.txt
stash@{1}: On main: Second Stash - newfile.txt
*/
```

`임시 저장소(Stash)` 값은 앞에 명시된 `stash@{0}` 인덱스값을 통해 접근할 수 있습니다. <br />
`임시 저장소(Stash)`에서 불러온 `stash`에 대한 작업을 완료하고 커밋을 했다면, 해당 `stash`를 삭제해주는 것이 좋습니다. 그렇지 않다면 계속 `Stash List`가 쌓여 관리가 힘들어질 수 있습니다.

```git
// 저장된 stash를 보고 싶은 경우 다음과 같이 인덱스값을 사용할 수 있습니다.
// git stash show stash@{1}
git stash show 1

// 저장된 stash를 로컬 폴더(Working Directory)에 반영해 보겠습니다.
git stash apply 1

// 반영한 stash를 제거해 보겠습니다.
git stash drop 1
// Dropped refs/stash@{1} (73a7797d74dec2fefeca848f2cd22e9bff2aa72e)

// 저장된 stash를 검토해보겠습니다.
// 앞서 1번 인덱스의 stash를 제거했기 때문에, 한 개의 stash만 존재합니다.
git stash list
// stash@{0}: On main: First Stash - audience.txt

// 임시 저장소 stash에 저장된 모든 내용을 제거해 보겠습니다
git stash clear

// stash apply + drop을 한 번에 하고 싶은 경우 pop 명령어를 사용할 수 있습니다.
git stash drop stash@{0}
```

## 5. Merging

<img style="width: 100vw;" src="https://cdn-images-1.medium.com/max/800/1*xJI1xHbnZNN7I-q7N1y7QA.jpeg" />

`merge`: 병합하다.

작업이 완료된 브랜치는 삭제되기 전 `master or main` 브랜치에 병합되어야 합니다. <br />
앞서 소개해 드린 선글라스와 카우보이모자를 착용한 문어가 병합의 예시가 될 수 있습니다.

`master or main` 브랜치는 소프트웨어 출시 혹은 배포할 때 사용하는 최종 결과물을 보관하는 대표 브랜치입니다.

`Merge(병합)`은 크게 두 종류가 존재합니다.

1. Fast-Forward Merges
2. Three-Way Merges

## 6. Fast-forward Merges

<img style="width: 100vw;" src="https://cdn-images-1.medium.com/max/800/0*CFU14gYcvrbSgcBk" />
<img style="width: 100vw;" src="https://cdn-images-1.medium.com/max/800/0*XdfIHTP87_ETNLL4" />

1. `Master` 브랜치가 세 개의 커밋을 한 시점에, `Bugfix` 브랜치를 생성했습니다.
2. `Bugfix`는 `Master` 브랜치가 생성한 세 개의 커밋에, 두 개의 커밋을 추가했습니다.
3. `Bugfix` 브랜치에서 모든 작업을 끝내고, 이를 `Master` 브랜치에 반영하고 싶은 경우,
4. `Master`를 가르치는 포인터를 다음 사진과 같이 `Bugfix` 브랜치가 있는 위치로 이동시킵니다.
5. `Master` 브랜치가 `Bugfix` 브랜치를 가르치는 상태에서 `Bugfix` 브랜치를 삭제하면, `Master` 브랜치만 남게 됩니다.

위 방식의 병합을 `Fast-Forward Merges`라 칭합니다.

<img style="width: 100vw;" src="https://cdn-images-1.medium.com/max/800/1*bFPYjQC8tlBDHFv9QNLVxg.png" />

`Fast-Forward Merges`를 조금 더 쉽게 이해하자면,

<img style="width: 100vw" src="https://cdn-images-1.medium.com/max/800/0*qDMElrC_GmMRzV5q" />
<img style="width: 100vw" src="https://cdn-images-1.medium.com/max/800/0*cf_aN7aSWirvAoUA" />
<img style="width: 100vw" src="https://cdn-images-1.medium.com/max/800/0*CNBK4I74HStffk2I" />

1. `v.1.0`의 `Master`폴더가 있습니다. `Bugfix`는 이 폴더를 그대로 복사합니다.
2. `Bugfix`는 복사한 폴더를 `v1.2`로 업데이트합니다.
3. `Bugfix`가 업데이트한 내용을 검토하고, 문제가 없다면 `Bugfix` 폴더 이름을 `Master`로 변경합니다.

`Fast-Forward Merges`를 구현해보겠습니다.

```git
// 0. 커밋 사항을 시각적인 그래프로 보고 싶은 경우 다음 명령어를 사용할 수 있습니다.
git log --oneline --all --graph --decorate

// 1. HEAD Pointer ==> bugfix/signup-form
git switch bugfix/signup-form

// 2. bugfix/signup-form에 두 개의 커밋을 추가하겠습니다.
echo a > a.txt

git add .
git commit -m "Merge Test Commit #1"

echo b > b.txt

git add .
git commit -m "Merge Test Commit #2"

// 3. HEAD Pointer ==> main
git switch main

// 4. Master브랜치와 bugfix/signup-form 브랜치를 Fast-Forward 방식으로 병합해 보겠습니다.
git merge bugfix/signup-form

// Updating 9a3133f..8cabf02
// Fast-forward
//  a.txt | 1 +
//  b.txt | 1 +
//  2 files changed, 2 insertions(+)
//  create mode 100644 a.txt
//  create mode 100644 b.txt
```

<img style="width: 100vw;" src="https://cdn-images-1.medium.com/max/800/0*tGbI4vC-_YCY87fK" />
<img style="width: 100vw;" src="https://cdn-images-1.medium.com/max/800/0*jMfODTG-FIivbW3R" />
<img style="width: 100vw;" src="https://cdn-images-1.medium.com/max/800/0*ZqHeKauMAqcGpbpm" />
<img style="width: 100vw;" src="https://cdn-images-1.medium.com/max/800/0*epH8Pb9Tle_Fqufh" />

`Fast-Forward Merges` 기술을 적용할 수 있는 상황임에도, 변경된 모든 사항을 기록하고자, 위 사진과 같이 새로운 커밋을 생성할 수 있습니다. <br />
이 경우 `git merge --no-ff <병합브랜치>` 명령어를 사용할 수 있습니다.

```git
// 1. bugfix/login-form 브랜치를 생성하고, 해당 브랜치로 전환해 보겠습니다.
git switch -C bugfix/login-form

// 2. c.txt 파일을 추가 후, 커밋을 하나 생성해보겠습니다.
echo c > c.txt

git add .
git commit -m "Update toc.txt"

// 3. 커밋 사항을 검토해보겠습니다.
git log --oneline --all --graph --decorate

// 4. HEAD Pointer ==> main
git switch main

// 5. Fast-Forward Merges 적용이 가능함에도, 새로운 커밋 생성하는 방식을 사용해보겠습니다.
// 새로운 커밋이기 때문에 커밋 메세지를 요구합니다.
git merge --no-ff bugfix/login-form

// 6. 커밋 사항을 검토해보겠습니다.
git log --oneline --all --graph --decorate
```

`Merge Commit`: `Fast-Forward-Merges`을 사용할 수 있음에도, 커밋 방식을 통해 만든 커밋을 `Merge Commit`이라 칭합니다. `Merge Commit` 사용 이유에는 의견이 분분합니다. `Merge Commit` 장단점을 알아보겠습니다.

- 장점:
  - 모든 기록이 추적되기 때문에 오히려 기록을 정확하게 잘 나타낸다는 주장도 있습니다. (True Reflection of History)
  - 이전 과정으로 돌아가기 용이하다는 장점이 있습니다. (Allow Reverting a feature)
- 단점
  - 사용 목적이 분명하지 않은경우 커밋 기록을 오염시킬 위험이 있습니다. (Pollutes the History)

`--graph` 속성을 통해 커밋 사항을 검토했을 때

`Fast-Forward Merges:` 일자 형태로 나오는 것을 확인할 수 있습니다. 검토하는 입장에서는 군더더기 없이 깔끔하지만, 정확히 어떤 과정을 통해 일자 형태가 형성되었는지가 생략되기 때문에, 모든 것을 기록하고 싶은 분은 `Merge Commit`을 선호하는 경향이 있습니다. 그렇지 않으면 대부분 `Fast-Forward Merges` 방식을 사용합니다.

---

Tip:

기본적으로 적용되는 `Fast-Forward-Merges` 속성을 해제하고 싶은 경우

```git
git config ff no

// 모든 저장소에 대해 해제하고 싶은 경우
git config --global ff no
```

---

## 7. Three-Way Merges

`Fast-Forward Merges`는 `Bugfix` 브랜치가 만들어진 시점부터, `Master` 브랜치가 별도의 커밋을 하지 않은 경우, 간단히 `Bugfix` 브랜치 이름을 `Master`로 변경하는 방식으로 브랜치를 병합하는 기술입니다. 이와 반대로, `Three-Way Merges`는 `Bugfix` 브랜치가 만들어진 이후, `Master` 브랜치에 추가 커밋이 발생했을 때 사용할 수 있는 병합 기술입니다.

<img style="width: 100vw" src="https://cdn-images-1.medium.com/max/800/0*994y8xZaVAUQvycS" />
<img style="width: 100vw" src="https://cdn-images-1.medium.com/max/800/0*VkBx-r0fJjqJQSdn" />
<img style="width: 100vw" src="https://cdn-images-1.medium.com/max/800/0*uhhhjZZQYBgY9VDJ" />

1. `Master` 브랜치가 세 개의 커밋을 한 시점에, `Bugfix` 브랜치를 생성했습니다.
2. `Bugfix`는 `Master` 브랜치가 생성한 세 개의 커밋에, 두 개의 커밋을 추가했습니다.
3. 이 시점에 `HEAD Pointer`를 `Master` 브랜치로 옮겨, 커밋을 하나 생성했습니다.
4. 더는 `Fast-Forward Merges` 방식으로 병합이 불가합니다. 왜냐하면, 해당 방식으로 병합하는 경우 `Master` 브랜치에 추가로 생성된 커밋이 소실되기 때문입니다.

<img style="width: 100vw" src="https://cdn-images-1.medium.com/max/800/0*BFetU7rbf0Mx37zb" />

5. `Master` 브랜치의 커밋이 소실되는 문제를 방지하면서, `Bugfix` 브랜치에 추가된 커밋을 동시에 반영할 때 `Three-Way Merges` 병합 기술을 이용할 수 있습니다. 위 사진을 보면 `Master` 브랜치와 `Bugfix` 브랜치가 공통으로 공유하고 있는 커밋을 빨간색 테두리로 표시했습니다.

<img style="width: 100vw" src="https://cdn-images-1.medium.com/max/800/0*2cWBRPTrb42My3WP" />
<img style="width: 100vw" src="https://cdn-images-1.medium.com/max/800/0*KAII0-JiszkTZPFA" />
<img style="width: 100vw" src="https://cdn-images-1.medium.com/max/800/0*RsgzB9p0hIMEBlbZ" />

6. 두 브랜치가 공통으로 공유하고 있는 커밋(빨간색 테두리)을 기준으로 각 브랜치가 마지막으로 커밋한 지점을 찾습니다.
7. 각 브랜치가 마지막으로 커밋한 커밋을 종합해 새로운 커밋을 하나 형성합니다. 이렇게 최종적으로 생성된(병합된) 커밋을 `Merge Commit`이라 칭합니다.

`Three-Way Merges`라는 명칭을 사용하는 이유는, 병합 과정에 적어도 세 개의 커밋이 필요하기 때문입니다.

`Merge Commit` = 공통 부모(Before Snapshot) + Master Commit(After Snapshot) + Bugfix Commit(After Snapshot)

1. 각 브랜치가 공통으로 공유하고 있는 커밋
2. `Master` 브랜치가 마지막으로 생성한 커밋
3. `Bugfix` 브랜치가 마지막으로 생성한 커밋

위 세개의 커밋을 병합해 최종적으로 `Merge Commit`을 구현할 수 있습니다. <br />

`Three-Ways Merges`를 구현해보겠습니다.

```git
// 1. 커밋 사항을 검토해보겠습니다.
git log --oneline --all --graph --decorate

// 2. HEAD ==> feature/change-password
git switch -C feature/change-password

// 3. change-password.txt 생성 후, 커밋을 하나 생성해보겠습니다.
echo hello > change-password.txt

git add .
git commit -m "Buld the change password"

// 4. 커밋 사항을 검토해보겠습니다.
git log --oneline --all --graph --decorate

// 5. HEAD ==> main
git switch main

// 6. objectives.txt 내용 업데이트 후, 커밋을 하나 생성해보겠습니다.
echo ** >> objectives.txt

git add .
git commit -m "Update Objectives.txt"

// 7. 커밋 사항을 검토해보겠습니다.
// main and feature/change-password 브랜치가 더는 일자 구조를 띠지 않는 것을 확인할 수 있습니다. 일자 구조를 Git에서는 Direct Linear Path라 칭합니다.
git log --oneline --all --graph --decorate

// 8. 이 시점에 feature/change-password 브랜치를 main 브랜치에 병합하게 되면 Three-Way Merges가 적용됩니다.
git merge feature/change-password

// 9. 커밋 사항을 검토해보겠습니다.
git log --oneline --all --graph --decorate
```

`Three-Way Merges` 요약

1. `main or master` 브랜치와 `feature/change-password` 브랜치 사이에 공통으로 존재하는 기준을 잡습니다. 해당 기준에서 각 브랜치의 마지막 커밋 지점을 검토합니다.
2. 브랜치 간의 공통점은 그대로 두고, 차이점을 비교해 병합 여부를 결정합니다.

## 8. Viewing Merged and Unmerged Branches

일반적으로 브랜치간의 병합을 끝내고, `main` 브랜치를 제외한 병합이 끝난 브랜치는 삭제해주는 것을 원칙으로 합니다. 이때 병합된 브랜치와 그렇지 않은 브랜치를 확인하고 싶을 때 다음 명령어를 사용할 수 있습니다.

```git
// 1. 병합된 브랜치를 확인하고 싶을 때
git branch --merged

// 2. 병합되지 않은 브랜치를 확인하고 싶을 때
git branch --no-merged
```

## 9. Merge Conflicts

병합 과정에 충돌이 발생할 수 있습니다. 병합 충돌 경우의 수는 크게 세 개가 있습니다.

1. 서로 다른 브랜치에서 같은 파일에 수정을 가한 경우.
2. 서로 다른 브랜치에서 같은 파일에 다른 작업이 발생한 경우 (한 곳은 삭제, 다른 한 곳은 수정).
3. 서로 다른 브랜치에서 같은 파일을 `Staging Area (git add)`에 추가한 경우 (파일명은 같지만, 그 내용은 다릅니다).

`Case #1`

```git
// 1. HEAD ==> bugfix/change-password
git switch -C bugfix/change-password

// 2. change-password.txt 내용 수정 후, 커밋을 하나 생성해보겠습니다. (change-password 브랜치)
echo bugfix/change-password >> change-password.txt

git add .
git commit -m "Build the change password"

// 3. HEAD ==> main
git switch main

// 4. change-password.txt 내용 수정 후, 커밋을 하나 생성해보겠습니다. (main 브랜치)
echo main >> change-password.txt

git add .
git commit -m "Build the change password"

// 5. bugfix/change-password 브랜치를 main 브랜치에 병합해보겠습니다.
git merge bugfix/change-password

// 병합 충돌이 발생한 것을 확인할 수 있습니다.
// Auto-merging change-password.txt
// CONFLICT (content): Merge conflict in change-password.txt
// Automatic merge failed; fix conflicts and then commit the result.


// 6. Working Directory를 검토해 보겠습니다.
git status

// 두 브랜치 모두 change-password.txt 파일을 수정해 충돌이 발생했습니다.
// both modified: change-password.txt

// 7. 문제 해결을 위해 change-password.txt를 검토해 보겠습니다.
code change-password.txt

// 다음과 같이 충돌 상황을 출력해줍니다.

/*
hello
<<<<<<<< HEAD (Current Change)
main
=======
bugfix/change-password
bugfix/change-password
>>>>>>>> bugfix/change-password (Incoming Change)
*/

// 8. 충돌 해결 후, 병합 커밋을 생성해보겠습니다.
git add .
git commit -m "Merge Conflict Solved"

// 9. 커밋 사항을 검토해보겠습니다.
git log --oneline --all --graph --decorate
```

`VSCode`는 충돌 문제 해결에 세 가지 대안을 제시합니다.

1. `Accept Current Change`: `main` 브랜치 수정 사항만 반영해 병합
2. `Accept Incoming Change`: `bugfix/change-password` 브랜치 수정 사항만 반영해 병합
3. `Accept Both Changes`: 두 브랜치 내용을 모두 합쳐 병합

## 10. Merge Tools

`Merge Confilct(병합 충돌)` 문제를 해결할 때 `VSCode` 등 유용하게 사용할 수 있는 시각화 도구가 존재합니다.

- Kdiff
- P4Merge
  - https://www.perforce.com/downloads/visual-merge-tool
- WinMerge (Windows Only)

## 11. Aborting a Merge

다른 브랜치와 `Commit Merge` 생성 중 충돌이 났을 때, `git merge --abort` 명령어를 사용해 병합 이전 시점으로 돌아갈 수 있습니다. <br />

`git merge --abort` 명령어는 충돌 해결에 시간이 충분하지 않을 때 사용할 수 있습니다.

```git
git merge --abort
```

## 12. Undoing a Faulty Merge

## 13. Squash Merging

## 14. Rebasing

## 15. Cherry Picking

## 16. Picking a File from Another Branch

## 17. Branching in VSCode
