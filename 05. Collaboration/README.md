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

## 07. Storing Credientials and Sharing Tags

`github tag`:

- 커밋을 한 시점 참조가 필요할 때 `Hash` 값 대신 알기 쉽도록 이름을 붙일 때 사용할 수 있습니다.
- 한 번 정한 태그 이름은, 브랜치처럼 위치가 이동이 불가하고, 고정됩니다.
- 깃에서 각 커밋에 정의할 수 있는 이름으로써, 주로 릴리즈 버전을 표시하는 데 사용합니다.
- 태그 여부와 이름에 따라 어떤 버전이 중요한 버전인지 파악할 수 있습니다.

`Release`는 유저들에게 소프트워어를 묶고 제공하는 `GitHub`의 방법입니다. 소프트웨어를 제공하기 위해 다운로드를 사용하는 것으로 대신으로 생각할 수 있습니다.

`Tag` 명령어를 통해 커밋에 별명을 설정할 수 있습니다. 하지만 일반적으로 `push` 명령어를 실행시 `Tag`는 중앙저장소에 반영되지 않습니다. 그러므로 `Tag`를 중앙저장소에 반영하기 위해서는 다음과 같이 별도로 `Tag`를 `push` 명령의 대상으로 명시해야합니다.

```bash
// v1.0 이름으로 현재 HEAD Pointer가 가르치고 있는 브랜치에 태그 추가
git tag v1.0

git log --oneline --all --graph

// v1.0 태그를 중앙저장소에 반영
git push origin v1.0

// 모든 태그를 반영하고 싶은 경우
git push origin --tags

// tag를 삭제하고 싶을 때 --delete 속성을 사용할 수 있습니다.
git push origin --delete v1.0

git log --oneline --all --graph

git tag -d v1.0
```

<img style="width: 100vw;" src="https://cdn-images-1.medium.com/max/800/1*wA0Ky--dqIelY8hJY3BmqA.png" />
<img style="width: 100vw;" src="https://cdn-images-1.medium.com/max/800/1*dF1Vg76afVNsMQOONo9Q4A.png" />
<img style="width: 100vw;" src="https://cdn-images-1.medium.com/max/800/1*xTUvgMSVzriW8-MSlNeScA.png" />

## 08. Releases and Sharing Branches

`깃허브(Github)`에는 릴리즈 기능이 있습니다다. 깃허브를 통해 협업을 하는 소스코드의 결과물을 공유할 수 있는 기능입니다.

<img style="width: 100vw;" src="https://cdn-images-1.medium.com/max/800/0*f6noMKwh7icYIiB7.png" />

1. `Github` 로그인 후 릴리즈 할 프로젝트를 선택합니다.
2. 상단에 `release` 탭을 클릭합니다.

<img style="width: 100vw;" src="https://cdn-images-1.medium.com/max/800/0*BkzlLEVM9U89IuEw.png" />

3. `Create a new Release`를 선택합니다.

<img style="width: 100vw;" src="https://cdn-images-1.medium.com/max/800/0*qMRFzAvOe8s98N6F.png" />

4. `Release` 작성 내용은 다음과 같습니다.

- 보통 버전명을 입력하고, 제목 및 내용을 작성합니다.
- `Pre-release`인지 아닌지 체크하는 것 또한 중요합니다.
- `tag` 이름과, `branch` 제목 및 상세 설명을 입력합니다. 사전에 빌드된 바이러니를 업로드 할 예정이라면 하단의 파일 첨부 부분에 끌어다 놓으면 됩니다.
- `Pre-release`: 공식적 배포 이전 노출시키는 것으로 베타버전을 생각할 수 있습니다.

5. `Publish Release`를 클릭하면 릴리즈가 완료됩니다.

`사용 목적`

태그와 릴리즈를 사용하면 소스의 버전 관리가 쉬워집니다. 이를 하나의 배포전략으로 적용해 특정시점으로 롤백하거나, 배포 버전을 생성하는 용도로 사용할 수 있습니다.

태그는 읽기전용 커밋이라 생각하면 이해가 쉽습니다. 커밋의 경우 내용 수정이 가능하지만, 태그는 수정할 수 없기 때문에 읽기전용 커밋의 개념이고, 소프트웨어의 새로운 버전을 릴리즈 할 때마다 사용할 수 있습니다.

Ex) 서비스1.0 버전이 릴리즈 될 때 태그해두고, 서비스1.1 버전을 개발하면서, 그 사이에 사용한 브래친와 커밋을 합쳐 서비스1.1 완성 버전에 태그를 적용하고 릴리즈 할 수 있습니다.

태그를 조회할 때는 태그들의 사전 순으로 정렬됩니다. 그러므로 태그명 그 자체가 버전을 나타낼 수 있습니다. 협업 시 특정 부분에 문제가 생겼을 때, 이전 태그를 전달하는 방식으로 문제를 해결할 수 있습니다. 또한 테스트 목적의 작업을 할 때 코드 복원의 목적으로 사용할 수 있습니다.

### Sharing Branches

로컬저장소에만 존재하는 브랜치를 중앙저장소에 반영하는 방법을 알아보겠습니다.

```bash
// 새로운 브랜치 생성 후 해당 브랜치로 전환
git switch -C feature/change-password

// 다음 오류는 feature/change-password 브랜치는 origin 브랜치와 연결되어 있지 않음을 의미합니다.
git push
/*
fatal: The current branch feature/change-password has no upstream branch.
To push the current branch and set the remote as upstream, use

    git push --set-upstream origin feature/change-password
*/

// main 브랜치는 origin/main과 연결된 반면에, feature/change-password 브랜치는 연결된 origin이 없습니다.
git branch -vv

// feature/change-password 브랜치를 origin과 연결하겠습니다.
git push --set-upstream origin feature/change-password

// 축약형
git push -u origin feature/change-password

git branch -vv

// remote tracked branch를 확인해보겠습니다.
git branch -r

// origin/HEAD -> origin/main
// origin/feature/change-password
// origin/main

// 브랜치를 삭제해보겠습니다.
git push -d origin feature/change-password

// remote tracked brach를 확인해보겠습니다.
git branch -r
/*
  origin/HEAD -> origin/main
  origin/main
*/

// 로컬저장소에는 여전히 브랜치가 존재합니다.
git branch -vv

// 로컬저장소에서 해당 브랜치를 삭제하겠습니다.
git switch main
git branch -d feature/change-password
```

## 09. Collaboration Workflow

<img style="width: 100vw;" src="https://cdn-images-1.medium.com/max/800/1*Mv30BvBIi-3Fmw1QGJKnOg.png" />
<img style="width: 100vw;" src="https://cdn-images-1.medium.com/max/800/1*ES1EO10qih3s7yUplZSPYw.png" />

1. `Github Repository`를 생성합니다.
2. `Github` 사이트에서 `feature/change-password` 브랜치를 생성합니다.
3. `This branch is even with master`의미는 생성한 `feature/change-password`브랜치가 `master` 브랜치와 차이가 없음을 의미합니다.
4. 로컬저장소로 돌아와 새로운 파일을 생성해 `master` 브랜치에 `push`를 하겠습니다.

```bash
git fetch

git branch
// * master

git branch -r
// origin/HEAD -> origin/master
// origin/feature/change-password
// origin/master

// 로컬 feature/change-password를 생성하고, origin/feature/change-password 브랜치와 맵핑하겠습니다.

// feature/change-password 브랜치에서 push되는 내용은 리모트 저장소인 origin/feature/change-password 저장소에 반영됩니다.

git switch -C feature/change-password origin/feature/change-password
```

5. 이 시점에 김아무개가 `Mars` 저장소를 클론해 협업에 참가했습니다.

```bash
git clone <저장소주소>

// feature/change-password 브랜치가 없는 것을 확인할 수 있습니다.
git branch
* master

// 로컬 feature/change-password를 생성하고, origin/feature/change-password 브랜치와 맵핑하겠습니다.

git switch -C feature/change-password origin/feature/change-password

echo password > file1.txt

git commit -am "Update file1"

git push
```

<img style="width: 100vw;" src="https://cdn-images-1.medium.com/max/800/1*jBf-BrBfCkc-RrjUl-0H0Q.png" />

6. 김아무개가 중앙저장소에 반영한 내용을 로컬저장소에 반영해보겠습니다.

```bash
git pull

// HEAD Pointer가 feature/change-password 브랜치를 가리키고 있는 것을 확인할 수 있습니다. 그 이유는 feature/change-password 브랜치는 master 브랜치와 똑같은 상태에서 새로운 작업을 했기 때문입니다. master 브랜치를 최신 상태로 유지하기 위해서는 feature/change-password 브랜치를 검토하고 변경된 내용을 병합해야 합니다.

git log --oneline --all --graph

git switch master
git merge feature/change-password

// HEAD Pointer가 master 브랜치를 가리키고 있습니다. 문제는 origin/master 브랜치는 여전히 이전 커밋에 위치해 있습니다. master 브랜치를 push 함으로써 이 문제를 해결할 수 있습니다.
git log --oneline --all --graph
// 73BB5F (HEAD => master)
// 478ac2c (tag: v1.0, origin/master, origin/HEAD)

git push

// master, origin/maaster, origin/feature/change-password 등 모든 브랜치의 싱크가 일치합니다.
git log --oneline --all --graph
// 73BB5F (HEAD => master, origin/master, origin/feature/change-password)

// feature/change-password 브랜치가 더 이상 필요 없기 때문에 삭제하겠습니다.
git push -d origin feature/change-password

// 로컬에서도 feature/change-password 브랜치를 삭제하겠습니다.
git branch -d feature/change-password

git branch
// * master

// 더는 origin/feature-change-password 브랜치가 존재하지 않습니다.
git branch -r
// origin/HEAD -> origin/master
// origin/master
```

7. 변경된 사항을 김아무게 로컬저장소에 반영해보겠습니다.

```bash
git pull

// 여전히 feature/change-password가 존재합니다.
git branch
// feature/change-password
// * master

// feature/change-password를 삭제하겠습니다.
git branch -d feature/change-password

// 리모트저장소 origin/feature/change-password 브랜치는 여전히 존재합니다.
git branch -r
// origin/HEAD -> origin/master
// origin/feature/change-password
// origin/master

// 리모트저장소 origin/feature/change-password 브랜치를 삭제하겠습니다.
git remote prune origin

// git branch -r
// origin/HEAD -> origin/master
// origin/master
```

## 10. Pull Requests

팀 단위 작업을 할 때 목적에 따라 여러 브랜치가 존재합니다. 이때 작업이 완료된 브랜치를 `master or main` 브랜치에 반영하기에 앞서, 여러 테스트 및 논의 과정이 필요합니다. 깃헙은 이 과정을 체계적으로 관리하는 `pull request` 기능을 제공합니다.

1. 김아무개 저장소에서 `feature/login` 브랜치를 생성해, 작업한 내용을 중앙저장소에 반영하겠습니다.

```bash
git switch -C feature/login

echo hello > file3.txt

git add .
git commit -m "Write hello to file3"

git push -u origin feature/login
```

<img style="width: 100vw;" src="https://cdn-images-1.medium.com/max/800/1*q9um_Rp9AJW5Jp32O7Vz3Q.png" />

`Compare & Pull request` 버튼을 클릭하거나, 직접 `Pull requests` 탭으로 이동해 `Pull request`를 생성할 수 있습니다.

1. Create Pull Request

<img style="width: 100vw;" src="https://cdn-images-1.medium.com/max/800/1*gLMs4eg3aIE_hPNgLufzVQ.png" />

`feature/login` 브랜치에는 파일 수정 외에는 복잡한 작업을 하지 않았기 때문에 `These branches can be automatically merged`라는 메세지가 출력됩니다. 스크롤을 내려보면 변경 사항을 검토할 수 있습니다.

<img style="width: 100vw;" src="https://cdn-images-1.medium.com/max/800/1*3ZC7JUKh_jRlBKJaLDi9Eg.png" />

`Create Pull Request` 버튼을 누르면 다음과 같이 병합에 대한 코멘트를 남길 수 있는 창이 출력됩니다. 조금 더 의미 있는 제목으로 변경해 보겠습니다.

<img style="width: 100vw;" src="https://cdn-images-1.medium.com/max/800/1*4sefKz3dONryAVJBQlCtSw.png" />

최종적으로 `Create Pull Request` 버튼을 클릭하면 다음 사진과 같이 결과값이 출력됩니다.

<img style="width: 100vw;" src="https://cdn-images-1.medium.com/max/800/1*uv01h9k4ogN1Axv_iNPVRw.png" />

오른쪽 탭 중 `reviewers` 탭을 클릭해 프로젝트 팀원 중 한 명을 등록하면 해당 팀원의 이메일로 검토를 기다린다는 연락이 전달됩니다 (Awaiting requested review from 본 계정).

본 계정으로 접속하면 김아무개가 요청한 `Pull Request`를 확인할 수 있습니다. 출력되는 메세지는 다음과 같습니다: `김아무개 requested your review on this pull request.`

검토를 원하는 경우 `Add your review` 버튼을 클릭합니다.

<img style="width: 100vw;" src="https://cdn-images-1.medium.com/max/800/1*zCw7arUbHaWanRCFMvMLuw.png" />

클릭 시 다음과 같이 검토할 수 있는 탭이 출력됩니다.

<img style="width: 100vw;" src="https://cdn-images-1.medium.com/max/800/1*hf5LyPETh3PP5NtIrGjW4g.png" />

변경 사항을 검토하고 다음과 같이 수정 사항을 전달할 수 있습니다.

<img style="width: 100vw;" src="https://cdn-images-1.medium.com/max/800/1*xBgxO1wCWSLAwpy5gYwSaA.png" />

`Start a review` 버튼을 클릭하면 다음 탭이 출력됩니다.

<img style="width: 100vw;" src="https://cdn-images-1.medium.com/max/800/1*rZCrgqQrvPEE9A1UknA2cw.png" />

`Finish your review` 버튼과 함께 최종 전달 사항을 작성할 수 있습니다. 만약 수정 요청 사항이 있는 경우 `Request changes` 항목을 클릭하고 리뷰를 전달할 수 있습니다.

<img style="width: 100vw;" src="https://cdn-images-1.medium.com/max/800/1*JLYvTfSbsyNXNwY3up1YnA.png" />

`Conversation` 탭을 방문하면 타임라인 방식으로 검토 사항을 확인할 수 있습니다.

<img style="width: 100vw;" src="https://cdn-images-1.medium.com/max/800/1*om2E7ysVoNfSr4a0lxvxsQ.png" />

김아무개는 본 계정에서 요청한 사항을 로컬에 반영하고 다시 `push`이후 `pull request`를 전달해보겠습니다.

```bash
// 김아무개

echo Hello > file3.txt

git commit -am "Capitalize Hello."

git push
```

김아무개는 `push`를 하고 `Reviewers` 탭에 순환 형태 버튼을 눌러 다시 검토(리뷰) 요청을 보냅니다.

<img style="width: 100vw;" src="https://cdn-images-1.medium.com/max/800/1*4n_cbVrlUpnaThRYoW1bhw.png" />

다시 본 계정으로 돌아오면 다음 알림이 출력됩니다.

<img style="width: 100vw;" src="https://cdn-images-1.medium.com/max/800/1*o8qelqBGTUerU1m7w9rPMw.png" />

김아무개가 수정한 내용이 괜찮다면 다음 메세지와 함께, `Approve` 항목을 선택 후 `Submit the review` 버튼을 클릭합니다.

<img style="width: 100vw;" src="https://cdn-images-1.medium.com/max/800/1*PpooPbSlwxlFfJNziGRfdw.png" />

`Conversation` 탭에 방문해보면, `Reviewers` 탭에 검토를 요청한 팀원에 체크가 출력된 것을 확인할 수 있습니다. 이는 `동의(Approve)`를 의미합니다.

<img style="width: 100vw;" src="https://cdn-images-1.medium.com/max/800/1*NWnQps3niMURh7-eSt1kmA.png" />

`Conversation` 탭 최하단으로 가보면 다음과 같이 `Merge pull request` 버튼을 확인할 수 있습니다. `Merge` 방식에는 세 개가 존재합니다.

<img style="width: 100vw;" src="https://cdn-images-1.medium.com/max/800/1*0lsWKjC4OtS4EDUjDZ1Xmw.png" />

<img style="width: 100vw;" src="https://cdn-images-1.medium.com/max/800/1*4TtYHbac-hInFizK5xrMSg.png" />

간단한 `simple commit merge`를 선택하고 `Merge Pull Request` 버튼을 누르면 ==> `confirm merge` 버튼이 출력되고, 이를 누르면 ==> `Pull request successfully merged and closed`가 출력되고 병합이 완료됩니다.

<img style="width: 100vw;" src="https://cdn-images-1.medium.com/max/800/1*7yNJJFS5LJXiCySNSbPXyQ.png" />

중앙저장소 반영 사항을 김아무개 로컬저장소에 반영해보겠습니다.

```bash
git switch master

git pull

git log --oneline --all --graph
// Merge pull request #1 from [name]/feature/login

// 병합이 끝났기 때문에 origin/feature/login 브랜치를 삭제하겠습니다.
git remote prune origin

git branch -r

git branch -d feature/login
```

## 11. Resolving Conflicts

```bash
// 김아무개
git switch -C feature/logout

echo hello > file1.txt

git commit -am "write hello to file1"

git push -u origin feature/logout
```

<img style="width: 100vw;" src="https://cdn-images-1.medium.com/max/800/1*9w17EgE9Xan8b7m2-g_wmg.png" />

`Compare & Pull Request`를 검토하기 전에, `master` 브랜치에 다른 변경 사항을 `push` 한 경우.

```bash
git switch master

echo world > file1.txt

git commit -am "write world to file1"
git push
```

`Compare & Pull Request`를 클릭하면 다음 오류가 출력됩니다: `Can't automatically merge`. 다음과 같이 제목을 변경하고 `Pull Request` 버튼을 클릭합니다.

<img style="width: 100vw;" src="https://cdn-images-1.medium.com/max/800/1*eHMJP3iKH65nxtOjttwM1g.png" />

<img style="width: 100vw;" src="https://cdn-images-1.medium.com/max/800/1*7GbfuCgLTPmS7OMAKZZ4PA.png" />

다음 탭에서 충돌 사항을 검토할 수 있는 항목이 출력됩니다.

<img style="width: 100vw;" src="https://cdn-images-1.medium.com/max/800/1*0VCK3weNFJAnIR7yQGi3iQ.png" />

`Resolve conflicts` 버튼을 클릭하면 충돌 난 파일을 검토할 수 있습니다. 어떤 내용을 반영할지 결정합니다.

<img style="width: 100vw;" src="https://cdn-images-1.medium.com/max/800/1*CPu840CzclTSj5bvswCFJQ.png" />

<img style="width: 100vw;" src="https://cdn-images-1.medium.com/max/800/1*IjGsctYrabkv-IhZ2pU2fQ.png" />

반영이 끝났다면, `Mark as resolved` 버튼을 클릭합니다. 이후 출력된 `Commit merge` 버튼을 클릭합니다.

<img style="width: 100vw;" src="https://cdn-images-1.medium.com/max/800/1*Peuq2LvpmRXm3K5QeF1p2Q.png" />

<img style="width: 100vw;" src="https://cdn-images-1.medium.com/max/800/1*AgcBzKB_nPnQ0r3G_3Uo6A.png" />

`Pull Requests` 탭을 확인해보면 다음 사진과 같이 충돌이 해결되고, `Merge Pull Request` 버튼이 활성화된 것을 확인할 수 있습니다. 최종적으로 병합이 완료됩니다. 이후 `pull` 명령어를 통해 병합된 데이터를 각자의 로컬저장소에 반영하면 싱크를 유지할 수 있습니다.

<img style="width: 100vw;" src="https://cdn-images-1.medium.com/max/800/1*4RsiSKchlWFRFkxBSDS17g.png" />

<img style="width: 100vw;" src="https://cdn-images-1.medium.com/max/800/1*L68hRbtTjCj4uKepvX-yGg.png" />

## 12. Issues, Labels and Milestones

## 13. Contributing to Open-Source Projects

## 14. Keeping a Forked Repository Up to Date

## 15. Collaboration Using VSCode

## Git Workflow Resources

- https://inpa.tistory.com/entry/GIT-%E2%9A%A1%EF%B8%8F-github-flow-git-flow-%F0%9F%93%88-%EB%B8%8C%EB%9E%9C%EC%B9%98-%EC%A0%84%EB%9E%B5
- https://techblog.woowahan.com/2553/
