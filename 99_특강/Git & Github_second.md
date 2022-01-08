# git & github 특강 2일차



## git 기본 설정

최초 한 번만 설정합니다. 매번 깃을 사용할 때마다 설정할 필요는 없습니다. 

1. 우선 누가 커밋 기록을 남겼는지 확인할 수 있도록 이름과 이메일을 설정해야합니다. 작성자를 수정하고 싶을 땐 이름, 메일 주소만 달리해 입력하면 됩니다.

   ```bash
   $ git config --global user.name "이름"
   $ git config --global user.email "메일 주소"
   ```

2. 작성자가 올바르게 작성됐는지 확인합니다.

   ```bash
   $ git config --global --list
   ```

   

## git 작동 방식

깃은 버전 관리 시스템이라고 했죠. 특정 상태(버전)를 기록합니다. 그리고 로컬환경에서 작동합니다. 그 후에 온라인 환경인 깃허브와 연결해야만 

공유되는 겁니다. 깃의 작동 방식을 살펴보죠.

![image](https://user-images.githubusercontent.com/96896885/148647306-44190a09-4f2e-4be5-813c-09810a5ae5a3.png)

깃 로컬 저장소는 크게 3 구간으로 나눌 수 있습니다. 버전 저장소까지 가야하는 일종의 여정이라고 볼 수 있습니다.

- `Working Directory` : 사용자가 일반적인 작업을 하는 곳
- `Staging Area` : 커밋을 위한 파일 및 폴더를 추가하는 곳
- `Local Repository` : staging area에 있던 파일 및 폴더의 변경사항(커밋)을 저장하는 곳

즉, **Working Director**y  ⇒  **Staging Area**  ⇒  **Local Repository** 과정으로 버전 관리를 수행합니다. 로컬환경에서 말이죠. 그럼 기본 명령어를 알아봅시다.





### 1. git init

```bash
$ git init
```

- 현재 작업 중인 디렉토리(폴더)를 깃으로 관리한다는 명령어입니다.
- `.git`이라는 숨긴 폴더를 만들고 터미널에는 `(master)`가 표기됩니다.
- 이미 깃 저장소인 폴더 안에서 또 다른 깃 저장소를 만들지 않도록 조심합니다.(터미널에 master가 있다면 입력하지 마세요❕❗) 
- 절대로 홈 디렉토리에서 git init을 하지 마세요. 모든 디렉토리를 깃을 관리하게 된답니다.(터미널 경로가 ~ 인지 확인합니다) 





### 2. git status

```bash
$ git status
```

- Working Directory와 Staging Area에 있는 파일의 현재 상태를 알려주는 명령어입니다.
- 어떤 작업을 시행하기 전에 수시로 status를 확인하면 좋습니다.
- 상태
  - `Untracked` : 깃이 관리하지 않는 파일 (한번도 Staging Area에 올라간 적 없는 파일)
  - `Tracked` : 깃이 관리하는 파일
    1. `Unmodified` : 최신 상태
    2. `Modified` : 수정되었지만 아직 Staging Area에는 반영하지 않은 상태
    3. `Staged` : Staging Area에 올라간 상태





### 3. git add

```bash
# 특정 파일
$ git add a.txt

# 특정 폴더
$ git add my_folder/

# 현재 디렉토리에 속한 파일/폴더 전부
$ git add .
```

- Working Directory에 있는 파일을 Staging Area로 올리는 명령어

- 깃이 해당 파일을 추적(관리)할 수 있도록 만듭니다.

- `Untracked, Modified → Staged` 로 상태를 변경합니다.

- 예시

  ```bash
  $ touch a.txt b.txt
  
  $ git status
  On branch master
  
  No commits yet
  
  Untracked files: # 트래킹 되고 있지 않는 파일 목록
    (use "git add <file>..." to include in what will be committed)
          a.txt
          b.txt
  
  nothing added to commit but untracked files present (use "git add" to track)
  # a.txt만 Staging Area에 올립니다.
  
  $ git add a.txt
  $ git status
  
  On branch master
  
  No commits yet
  
  Changes to be committed: # 커밋 예정인 변경사항(Staging Area)
    (use "git rm --cached <file>..." to unstage)
          new file:   a.txt
  
  Untracked files: # 트래킹 되고 있지 않은 파일
    (use "git add <file>..." to include in what will be committed)
          b.txt
  ```





### 4. git commit

```bash
$ git commit -m "first commit"
[master (root-commit) c02659f] first commit
 1 file changed, 0 insertions(+), 0 deletions(-)
 create mode 100644 a.txt
```

- Staging Area에 올라온 파일의 변경 사항을 하나의 버전(커밋)으로 저장하는 명령어
- `커밋 메세지`는 현재 변경 사항들을 잘 나타낼 수 있도록 `의미` 있게 작성하는 것을 권장합니다.
- 각각의 커밋은 `SHA-1` 알고리즘에 의해 반환 된 고유의 해시 값을 ID로 가집니다.
- `(root-commit)` 은 해당 커밋이 최초의 커밋 일 때만 표시됩니다. 이후 커밋부터는 사라집니다.





### 5. git log

```bash
$ git log
commit 1870222981b4731d14ef91d401c68c0bbb2f6e7d (HEAD -> master)
Author: kyle <kyle123@hphk.kr>
Date:   Thu Dec 9 15:26:46 2021 +0900

    first commit
```

- 커밋의 내역(`ID, 작성자, 시간, 메세지 등`)을 조회할 수 있는 명령어
- 옵션
  - `--oneline` : 한 줄로 축약해서 보여줍니다.
  - `--graph` : 브랜치와 머지 내역을 그래프로 보여줍니다.
  - `--all` : 현재 브랜치를 포함한 모든 브랜치의 내역을 보여줍니다.
  - `--reverse` : 커밋 내역의 순서를 반대로 보여줍니다. (최신이 가장 아래)
  - `-p` : 파일의 변경 내용도 같이 보여줍니다.
  - `-2` : 원하는 갯수 만큼의 내역을 보여줍니다. (2 말고 임의의 숫자 사용 가능)







## PUSH

![image1](https://user-images.githubusercontent.com/96896885/148647323-700562f8-b02e-4cf4-b2e2-0929d56faffb.png)


이제 로컬환경에서 버전관리를 했다면 온라인 환경과 연동 해야합니다. 깃허브에서 레포지터리 즉, 방 하나를 파고 그 주소를 깃과 연결하면 끝.

연결하는 방법은 다음과 같습니다.

1. 내가 만든 방 주소를 가져옵니다.
2. 터미널에 `git remote add origin`을 쓰고 방 주소를 씁니다.
3. `git remote -v`를 칩니다.
4. 이제 온라인 환경에 올려줍니다.`git push origin master`을 입력하고 터미널에 master ⇒ master가 나오면 성공.







