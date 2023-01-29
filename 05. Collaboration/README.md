# Collaboration

1. Collaboration Workflows
2. Pushing, Fetching, and Pulling
3. Pull Requests, issues and milestones
4. Contributing to open-source Projects

## 1. Collaboration Workflows

<img style="width: 100vw;" src="https://cdn-images-1.medium.com/max/800/0*kf-_cw5f9oqJKfUg" />

버전 관리 시스템은 위 사진과 같이 두 종류가 존재합니다.

1. Centralized (중앙형)
2. Distributed (분산형)

중앙형 버전 관리 시스템은 프로젝트에 참여한 모든 사람이 하나의 저장소(중앙 저장소)에 모든 내용을 저장합니다. <br />
문제는 중앙 저장소를 담당하는 서버가 오프라인 상태이거나 문제가 발생한 경우, 변경 사항을 반영할 수 없다는 점입니다.

분산형 버전 관리 시스템은, 반면에, 프로젝트에 참여한 모든 사람의 컴퓨터에 변경 사항 반영에 사용할 수 있는 저장소가 존재합니다. 중앙 서버에 의존하는 방식이 아니므로 오프라인 혹은 다른 문제가 발생해도 변경 사항 반영을 이어나갈 수 있습니다.

분산형 버전 관리 시스템 방식으로 협업 시, 사진과 같이 `Local Repository`간의 싱크를 맞춰야 합니다. 문제는 이 과정이 너무 복잡하고, 오류가 발생할 확률이 높습니다.

분산형 버전 관리 방식과 중앙형 관리 방식을 조합해 분산형 버전 관리 협업 시스템의 복잡도와 오류 문제의 대안으로 사용할 수 있습니다. 이 대안의 이름은 `Centralized Workflow`입니다.

1. 모든 사람의 컴퓨터에 변경 사항을 반영할 수 있는 저장소 존재
2. 모든 사람의 작업 내용을 합치고 싱크를 맞추는 목적의 중앙 저장소 존재

### Centralized Workflow

<img style="width: 100vw;" src="https://cdn-images-1.medium.com/max/800/0*gCKNQaQKOWQUbOT1" />

<img style="width: 100vw;" src="https://cdn-images-1.medium.com/max/800/0*Q1vmsjpHZLvy6IaC" />

`노란색 원통`: 모든 사람이 각자의 작업 사항을 기록할 수 있는 저장소입니다.

`보라색 원통`: 사람들이 작업한 내용 간의 동기화를 위해 사용하는 중앙 저장소입니다.

겉보기에 중앙형 버전 관리 시스템과 차이가 없어 보일 수 있습니다.

이 방식은 개인팀에서 주로 사용되며 장점은 첫 번째 사진과 같이 모든 사람이 각자의 작업 사항을 기록할 수 있는 저장소가 있기 때문에, 두 번째 사진과 같이 중앙 저장소에 문제가 생겨 변경 사항 공유가 불가한 경우, 중앙 저장소를 거치지 않고 각 저장소 간의 직접적인 작업 사항 교환을 통해 싱크를 유지할 수 있습니다.

<img style="width: 100vw;" src="https://cdn-images-1.medium.com/max/800/0*kY3y4a82lra5wlLK" />

이와 같은 방식의 협업 구조에서 중앙 저장소는 크게 두 장소에 배치합니다.

1. 개인 서버(Private Server)
2. 클라우드 서비스(Cloud Service)

- Ex) Github, GitLab, GitBucket

### Centralized Workflow 활용 시나리오

<img style="width: 100vw;" src="https://cdn-images-1.medium.com/max/800/0*FL28jm_R-S2QZQGc" />

<img style="width: 100vw;" src="https://cdn-images-1.medium.com/max/800/0*kZgtws8_QqnpAFnu" />

<img style="width: 100vw;" src="https://cdn-images-1.medium.com/max/800/0*LVvcBX1mkaDs3shV" />

1. `John과 Amy`과 협업을 하기 위해 중앙 저장소를 하나 생성했습니다. (첫 번째 사진)
2. `John과 Amy`의 컴퓨터에 중앙 저장소 내용을 그대로 복사하고자 `clone` 명령어를 사용했습니다. (첫 번째 사진)

- `clone` 명령어를 통해 각자의 작업 사항을 기록할 수 있는 저장소를 생성했습니다. (Local Repository 생성)

3. `John`은 일정 단위의 작업을 하고 커밋 3개를 생성하고, 이 내용을 `Amy`와 공유하고자 중앙 저장소에 `push` 명령어를 통해 생성한 3개의 커밋을 전달했습니다. (두 번째 사진)

- `John`이 중앙 저장소에 반영하는 동안, `Amy`가 `clone` 명령어를 통해 중앙 저장소 내용을 복사한 이후로 어떠한 작업도 하지 않았다는 가정하에 설명하겠습니다. (두 번째 사진)

4. `John`이 `push` 명령어를 통해 변경 사항을 중앙 저장소에 반영함으로써 `John`과 중앙 저장소는 싱크가 맞는 상태입니다. (두번째 사진)

5. `Amy` 또한 `John`의 반영 사실을 듣고 중앙 저장소에 있는 내용을 `pull` 명령어를 통해 반영합니다. `clone` 명렁어는 중앙 저장소를 복사함과 동시에 `Amy` 저장소와 서로 연결된 길을 만들어 주는 역할을 합니다. 그러므로 최초 `clone` 이후에 데이터를 주고받을 때는 `push and pull` 명령어를 이용합니다. (세 번째 사진)

6. 결과적으로 `John == 중앙 저장소 == Amy`는 싱크가 맞는 상태가 되었습니다. (세 번째 사진)

`Centralized Workflow`는 대게 개인 팀 단위로 작업할 때 많이 사용하는 구조입니다. 이와 더불어 오픈소스와 같이 수많은 사람이 프로젝트에 기여할 때 모두가 중앙 저장소에 `push and pull`을 할 수 있다면 심각한 문제가 발생할 수 있습니다. 이러한 문제를 방지하고자 오픈소스 프로젝트를 할 때는 `Integration-Manager Workflow`를 사용합니다.

### Integration Manager Workflow

<img style="width: 100vw;" src="https://cdn-images-1.medium.com/max/800/0*FOgr6YMv8TSZ3Gg4" />
<img style="width: 100vw;" src="https://cdn-images-1.medium.com/max/800/0*mxjJ-9yWGrhG6L-H" />
<img style="width: 100vw;" src="https://cdn-images-1.medium.com/max/800/0*j-pV1fo5Rm-77kjC" />
<img style="width: 100vw;" src="https://cdn-images-1.medium.com/max/800/0*1TlmLf9AuIwVithK" />
<img style="width: 100vw:" src="https://cdn-images-1.medium.com/max/800/1*dhMPQtcMwpAt_sJ1TpdVaw.png" />
<img style="width: 100vw;" src="https://cdn-images-1.medium.com/max/800/0*UCSw_Z702hcn1cOt" />
<img style="width: 100vw;" src="https://cdn-images-1.medium.com/max/800/0*LGc0XuUoK3RLTzUn" />
<img style="width: 100vw;" src="https://cdn-images-1.medium.com/max/800/0*Z9WiInHwz-wSjdYq" />

오픈소스 프로젝트는 소유하고 유지하는 `메인테이너(Maintainer)`와 `기여자(Contributor)`로 구성됩니다. 문제는 기여자가 누군지 모른다는 점에서 발생합니다. 신뢰할 수 없는 기여자 중앙 저장소에 코드를 배포할 수 있다면 프로젝트는 순식간에 엉망이 될 수 있습니다.

다시 말해서 기여자는 직접 오픈소스 프로젝트 중앙 저장소에 `push`를 할 수 없습니다. 오직 메인테이너만 프로젝트 중앙 저장소에 `push`할 수 있는 권한이 있습니다.

메인테이너가 존재하는 오픈소스 프로젝트에 기여하고 싶다면 `Integration Manager Workflow` 방식을 따라야 합니다.

1. `기여자(Contributor)`는 클라우드 상에서(Github)에서 오픈소스 프로젝트 저장소를, `기여자(Contributor)` 클라우드(Github) 복제합니다. 이때 `Fork` 명령어를 사용합니다. (두 번째 사진)

- 오픈소스 저장소 이름: open-source ==> `Fork` 명령어 실행 ==> `기여자-open-soruce` 저장소에 클라우드(Github)에 생성됩니다.

2. `기여자(Contributor)` 컴퓨터에 `기여자-open-source` 저장소를 `clone` 명령어를 사용해 저장소를 복제하고 `push and pull` 명령어를 사용할 수 있는 길을 만듭니다. (세 번째 사진)

3. `기여자(Contributor)`가 오픈소스 프로젝트에 기여하고 싶은 부분을 추가 및 수정 후에 `push` 명령어로 `기여자-open-soruce` 저장소에 반영합니다. (네 번째 사진)

4. `기여자(Contributor)`는 추가 및 수정한 내용이 반영된 `기여자-open-source` 저장소 내용과 함께 해당 오픈소스 `메인테이너(Maintainer)`에게 연락을 취합니다. 이때 연락을 전문 영어로 `pull request`라고 합니다. 말 그대로 내가 추가 및 수정한 내용을 검토하고 `pull` 명령어를 통해 `메인테이너(Maintainer) Local Repository`에 반영해달라는 요청입니다. 바로 중앙 저장소에 반영하지 않는 이유는, `메인테이너(Maintainer) Local Repository`에서 `push` 명령어를 통해 오픈 소스 중앙 저장소에 반영해야지만 싱크를 유지할 수 있기 때문입니다. (다섯 번째 사진)

- `Pull Request`는 `Github`에서 제공하는 기능입니다.

5. `기여자(Contributor)` 추가 및 수정 사항을 검토하고, `메인테이너(Maintainer)`는 `Pull` 명령어를 통해 `Local Repostiory`에 `기여자-open-source` 저장소 내용을 반영합니다. (여섯 번째 사진)

6. `메인테이너(Maintainer)`는 최종적으로 수정된 내용을 `push` 명령어를 통해 오픈소스 저장소에 반영합니다 (일곱 번째 사진)

7. 새로운 `기여자(Contributor)`가 오픈 소스에 기여하고 싶다면, 마지막 사진과 같이 `Fork` 명령어를 통해 저장소를 복사하고, 1 ~ 6번 순서로 추가 및 수정 사항을 오픈소스 저장소에 반영할 수 있습니다.

## 02. Creating a Github Repository

1. https://github.com/
2. Mars 이름으로 리파지토리 생성
3. Add a README file 선택
4. 생성된 repository의 url 확인하기

`협업자(Collaborators)` 등록을 원하는 경우

1. settings
2. Collaborators
3. Manage Access
4. Add people

## 03. Cloning a Repository

`git clone <주소>`: 클라우드 혹은 온라인 저장소 `Remote Repository`를 내 컴퓨터에 복사하고, 변경 사항을 서로 주고받는 길을 생성할 때 사용하는 명령어입니다.

```cmd
git clone https://github.com/jos50275266/Mars.git

// 이름을 변경하고 싶은 경우
git clone https://github.com/jos50275266/Mars.git MarsProjet

git log --oneline --all --graph
// 아래와 같이 여러 개의 브랜치가 존재하는 것을 확인할 수 있다.
// * f447a1d (HEAD -> main, origin/main, origin/HEAD) Initial commit
```

## 04. Fetching

`git fetch`: `clone` 명령어 실행후 `중앙저장소(Remote Repository)`에 변경된 내용을 `로컬저장소(Local Repository)`에 다운로드할 때 사용하는 명령어입니다.

<img style="width: 100vw;" src="https://cdn-images-1.medium.com/max/800/0*9MhF_5435NOQmLWL" />
<img style="width: 100vw;" src="https://cdn-images-1.medium.com/max/800/0*oN0dMgre2n2cfHbJ" />
<img style="width: 100vw;" src="https://cdn-images-1.medium.com/max/800/0*O5biR52c2T84I-DL" />
<img style="width: 100vw;" src="https://cdn-images-1.medium.com/max/800/0*Gks5DOTvSkdMOqTf" />

`Clone` 명령어를 통해 깃허브 `중앙저장소(Remote Repository)`를 복사함과 동시에 깃허브와 `로컬 저장소(Working Directory(Local Repository))` 사이에 연결된 길을 만들었습니다.

로컬 저장소에서 `A` 커밋 부터 작업을 진행하려는데, 중앙저장소에 `B` 커밋이 추가된 소식을 들었습니다. 만약 로컬 저장소에서 `A ==> C` 작업 이후에 `push` 명령어를 통해 중앙저장소에 반영하면, 충돌이 발생합니다. 이와 같은 문제 발생을 방지하고자, `fetch` 명령어를 통해 중앙저장소에 추가된 내용을 로컬 저장소에 다운로드 할 수 있습니다.

`fetch` 명령어를 실행하면, 중앙저장소를 추적하는 `origin/MASTER` 포인터는 다운로드해온 `B` 커밋을 가리키게 됩니다. 하지만 문제는 로컬저장소에는 업데이트가 반영되지 않아, 여전히 `A` 커밋(스냅샷)을 가리키고 있습니다.

`fetch` 명렁어를 통해 업데이트된 중앙저장소 내용을 로컬 저장소에 다운로드했다면, `merge` 명령어를 통해 `MASTER` 브랜치를 `origin/MASTER` 브랜치에 병합해 중앙저장소와 싱크를 맞추고 작업을 이어나가야 합니다.

`Fetching Exercise`

1. Github Repository
2. README.md 수정
3. Commit Changes (Commit Directly to the master branch)

```bash
git log --oneline --all --graph

// 중앙저장소에 있는 내용을 master 브랜치로 다운로드하기
git fetch

git log --oneline --all --graph

// 로컬저장소와 중앙저장소를 비교해줍니다.
git branch -vv

git merge origin/master
// Fast-forward

git log --oneline --all --graph

// 로컬저장소와 중앙저장소를 비교해줍니다.
git branch -vv

cat README.md
```

## 05. Pulling

<img style="width: 100vw;" src="https://cdn-images-1.medium.com/max/800/0*oBIya6-v_JBz-83L" />
<img style="width: 100vw;" src="https://cdn-images-1.medium.com/max/800/0*1JauHm9WGus1SbtY" />
<img style="width: 100vw;" src="https://cdn-images-1.medium.com/max/800/0*2ZjTJEAV2VCO2xI8" />
<img style="width: 100vw;" src="https://cdn-images-1.medium.com/max/800/0*i44N41QQRRUT7_yB" />
<img style="width: 100vw;" src="https://cdn-images-1.medium.com/max/800/0*m2cRqSVYiNRqyhJp" />
<img style="width: 100vw;" src="https://cdn-images-1.medium.com/max/800/0*1STDCBZKAi8DGfK2" />

`fetch` 명령어를 사용하면 추가로 `merge` 명령어를 사용해 다운로드한 내용을 반영해줘야 합니다. `pull` 명령어를 통해 이 두 단계를 한 번에 구현할 수 있습니다.

`Clone` 명령어를 통해 깃허브 `중앙저장소(Remote Repository)`를 복사함과 동시에 깃허브와 `로컬 저장소(Working Directory(Local Repository))` 사이에 연결된 길을 만들었습니다.

로컬저장소에서 `B` 커밋을 추가로 생성했고, 중앙저장소에서 `C` 커밋을 생성했습니다. 이 경우 로컬저장소가 `push` 명령어로 중앙저장소를 반영하면, 충돌이 발생합니다.

이러한 충돌 상황에 `push` 명령을 실행하기 전, `pull` 명령어를 실행하면 `C` 커밋을 다운로드해 `MASTER` 브랜치에 연결하지 않고 `origin/MASTER` 브랜치를 가리키게 합니다. 이후 깃은 병합을 위해 `Three-Way Merges`를 적용해 `D`라는 새로운 커밋을 생성합니다.

하지만 작업 기록을 오염시킨다는 점에서 `Three-Way Merges` 방식의 병합을 선호하지 않을 수 있습니다. 이 경우 `rebase` 명령어를 통해 문제를 해결할 수 있습니다. `B`와 `C` 커밋 모두 `A` 커밋에 의존하고 있고, 두 커밋 사이에 겹치는 내용이 없다고 가정해보겠습니다.

<img style="width: 100vw;" src="https://cdn-images-1.medium.com/max/800/0*6J2xPVp2FzfkMgFn" />
<img style="width: 100vw;" src="https://cdn-images-1.medium.com/max/800/0*IoalCUdfPNBkDWyE" />
<img style="width: 100vw;" src="https://cdn-images-1.medium.com/max/800/0*9_YcBw1UTCrCTOO8" />
<img style="width: 100vw;" src="https://cdn-images-1.medium.com/max/800/0*ut1RybtHGJTSlnFx" />

`pull --rebase` 명령어를 통해 기록이 오염되는 문제를 해결할 수 있습니다.
(단, 주의해야 할 점은 `rebase` 사용시 `origin/MASTER` 브랜치 위에 `MASTER` 브랜치가 병합된다는 점입니다)

`Pull Exercise`

1. Github Repository
2. README.md 파일 수정
3. 다음 코드 실행

```bash
echo hello > file1.txt

git add .
git commit -m "Add File1"

git log --oneline --all --graph
// * be61457 (HEAD -> main) Add file1.txt
// * ffc35e4 (origin/main, origin/HEAD) Update README.md
// * f447a1d Initial commit

git pull
/*
- 아래와 같이 Non-Linear History가 형성된 것을 확인할 수 있다.
*   cf7aa42 (HEAD -> main) Merge branch 'main' of https://github.com/jos50275266/Mars into main
|\
| * e5d53d6 (origin/main, origin/HEAD) Update README.md
* | be61457 Add file1.txt
|/
* ffc35e4 Update README.md
* f447a1d Initial commit
*/
```

`pull` 명령어도 병합의 일종이기 때문에 `reset` 명령어를 통해 이전 상태로 되돌릴 수 있습니다.
이전 상태로 되돌려 `--rebase`를 적용해보겠습니다.

```bash
git reset --hard HEAD~1

git log --oneline --all --graph
/*

* be61457 (HEAD -> main) Add file1.txt
| * e5d53d6 (origin/main, origin/HEAD) Update README.md
|/
* ffc35e4 Update README.md
* f447a1d Initial commit

*/

git pull --rebase
/*
- Linear 형태를 띠고 있는 것을 알 수 있습니다.
* 61bc3ef (HEAD -> main) Add file1.txt
* e5d53d6 (origin/main, origin/HEAD) Update README.md
* ffc35e4 Update README.md
* f447a1d Initial commit
*/
```

## 06. Pushing

<img style="width: 100vw;" src="https://cdn-images-1.medium.com/max/800/0*KHYTXKtP28fzqdVQ" />
<img style="width: 100vw;" src="https://cdn-images-1.medium.com/max/800/0*zYECvL5vErqFIeaF" />
<img style="width: 100vw;" src="https://cdn-images-1.medium.com/max/800/0*imWXcRiNYYct-0Vh" />
<img style="width: 100vw;" src="https://cdn-images-1.medium.com/max/800/0*FxTRAWb8bx3vGXu8" />

`Clone` 명령어를 통해 깃허브 `중앙저장소(Remote Repository)`를 복사함과 동시에 깃허브와 `로컬 저장소(Working Directory(Local Repository))` 사이에 연결된 길을 만들었습니다.

사진을 보면 `MASTER` 브랜치가 `origin/MASTER` 브랜치보다 한 커밋 앞서 있습니다. 또한 중앙저장소에는 로컬저장소의 변경 사항이 반영되지 않았습니다. `push` 명령어를 통해 로컬저장소의 변경 사항을 중앙저장소에 반영할 수 있습니다.

`push` 명령어를 실행하면, 로컬저장소 내용이 중앙저장소에 반영되고 중앙저장소 상태를 추적하는 `origin/MASTER` 포인터 또한 로컬저장소의 최신 커밋은 `MASTER` 브랜치가 가리키고 있는 곳을 가리키게 됩니다.

`Pushing Exercise`

```bash
// origin = 중앙저장소(remote repository)를 의미합니다
git push origin master

// origin이 기본값이기 때문에 생략도 가능합니다.
git push

// Github Repository를 확인해보면 file1.txt 파일이 추가되어있습니다.
```

<img style="width: 100vw;" src="https://cdn-images-1.medium.com/max/800/0*g2c0T0PDeipvtV77" />
<img style="width: 100vw;" src="https://cdn-images-1.medium.com/max/800/0*BGu7hnq5PIENTGUx" />
<img style="width: 100vw;" src="https://cdn-images-1.medium.com/max/800/0*_zycfHQaEQ5okeLZ" />
<img style="width: 100vw;" src="https://cdn-images-1.medium.com/max/800/0*RUTUHlDxCoVPvqTZ" />
<img style="width: 100vw;" src="https://cdn-images-1.medium.com/max/800/1*q9ZE5Ia7AlgB7S_g31Pvdg.png" />

`Push` 명령어를 실행하려 하는데, 위 사진과 같이 중앙저장소에 `D` 커밋이 추가되어 있다면 어떻게 이 문제를 해결할 수 있을까요?

해결책1: `git push -f`

- 해당 명령어는 중앙저장소에 내용을 무시하고 로컬저장소에 작업한 내용을 중앙저장소에 반영하는 방법입니다. (명확한 이유가 없는 한 절대 사용하지 않습니다).

해결책2: `pull` ==> `push`

- `pull` 명령어를 통해 중앙저장소 내용을 다운로드 및 병합을 진행하고, 싱크를 맞춘 상태에서 `push` 명령어를 실행합니다.

## 07. Storing Credientials and Tags

## 08. Releases and Sharing Branches

## 09. Collaboration Workflow

## 10. Pull Requests

## 11. Resolving Conflicts

## 12. Issues, Labels and Milestones

## 13. Contributing to Open-Source Projects

## 14. Keeping a Forked Repository Up to Date

## 15. Collaboration Using VSCode
