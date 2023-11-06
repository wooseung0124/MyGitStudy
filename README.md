# 20231020

버전관리, 협업, 소셜 코딩... => git으로 사용

*git 은 oracle과는 다르게 대소문자 구분함

application 실행시
1. gui에서 아이콘 더블 클릭
2. command prompt or power shell 에서 실행

설치여부 확인
시작 - 프롬프트 - git
ㄴ> .exe는 생략가능
ㄴ> 설치여부는 확인해주되 바로 종료됨

명령 프롬프트는 마우스 없이 작동시킬 줄 알아야 한다. 마우스가 없기 때문이다.

사용법
실행 : [운영프로그램]+[실행 option]
ㄴ> ex) 메모장 파일 만들기 : C:\Users\acorn>memo f -n
ㄴ> 문법 : c드라이브/사용자(User)/컴퓨터 사용자 계정/메모장 파일(f) 새로 만들기(n)

git 사용법
1. 사용자 이름과 이메일 설정하기
C:\Users\acorn>git config --global user.name "leeseungwoo"
C:\Users\acorn>git config --global user.email "oy10302@naver.com"
ㄴ> 띄어쓰기 틀리면 오류남

git으로 코드 관리법
ㄴ>실습을 위해 폴더와 파일 만들어두기 : C:\acorn202310\git_test

원하는 파일 경로 이동법 : 체인지 디렉토리(cd)
C:\Users\acorn>cd C:\acorn202310\git_test

상태확인
C:\acorn202310\git_test>git status
ㄴ> 결과값 : fatal: not a git repository (or any of the parent directories): .git
ㄴ> 에러발생

관리설정
C:\acorn202310\git_test>git init
ㄴ> 결과값 : Initialized empty Git repository in C:/acorn202310/git_test/.git/
ㄴ> .git/ : 숨김폴더 생성됨
ㄴ> 육안으로 확인하는 법 : 경로를 따라 파일 열기 - '보기' - '숨긴 항목' 체크
ㄴ> 다시 status 명령어를 실행하면 결과값이 다르게 나옴
C:\acorn202310\git_test>git status
On branch master

No commits yet

Untracked files:
  (use "git add <file>..." to include in what will be committed)
        20231020.txt
        index.html

nothing added to commit but untracked files present (use "git add" to track)
ㄴ> 해석하면 다음과 같다.
ㄴ> On branch master => master(branch 포인터)가 생성되었다. => branch: 가지
ㄴ> master은 일종의 스냅샷이다. 게임으로 치면 세이프존. 필요할 때 되돌아갈 수 있음
ㄴ> Untracked files : 사진에 한 번도 안 찍은 파일
ㄴ> 되돌아갈 수 없는 상태

master 기록법(세이프존 만들기)
C:\acorn202310\git_test>git add index.html
ㄴ> 결과값 :
Changes to be committed:
  (use "git rm --cached <file>..." to unstage)
        new file:   index.html
ㄴ> Untracked files에서 Changes to be committed로 바뀜

세이프존 저장하기
C:\acorn202310\git_test>git commit -m "index.html added"
ㄴ> 문법 : git commit -m ["저장명"]

세이프존 기록보기
C:\acorn202310\git_test>git log
ㄴ> 결과값:
commit c54abcabf233643347f287034227a9e15c8cd886 (HEAD -> master)
Author: leeseungwoo <oy10302@naver.com>
Date:   Fri Oct 20 10:49:38 2023 +0900

    index.html added
ㄴ> commit c54abcabf233643347f287034227a9e15c8cd886 (HEAD -> master)
ㄴ> 해석 : commit 의 id
ㄴ> 상태 : commit이라는 사진(현시점)을 master라는 포인터(세이프존)가 지정되었고 
 head라는 커서가 올려짐

*커서 : head 위치에 따라 파일이 변화할 수 있다.

실습하기 : 임의의 파일을 내용 수정하고 똑같이 세이프존 진행

이전 세이프존으로 돌아가기
C:\acorn202310\git_test>git checkout head~
ㄴ> 상태 : master는 여전히 마지막에 기록한 파일에 지정된 상태지만 head 커서를 이전으로 옮김
ㄴ> 비쥬얼 스튜디오 코드로 확인해보기

다시 최근 세이프존으로 가기
C:\acorn202310\git_test>git checkout master
ㄴ> 비쥬얼 스튜디오 코드로 확인해보기

실습하기 : 임의의 파일 내에 링크기능 부여하고 링크를 타고 이동할 새로운 파일 생성하기

모든 변경사항 모두 저장하기
C:\acorn202310\git_test>git add .
ㄴ> 그리고 세이프존 저장하기

commit(세이프존) 취소하기
C:\acorn202310\git_test>git reset --hard HEAD~

commit(직전 세이프존) 복구하기
C:\acorn202310\git_test>git reset --hard ORIG_HEAD

# 20231023

C:\Users\acorn>
ㄴ> 해설: 파일탐색기 열람시 확인되는 파일 경로

local Repository : 사진찍는 곳

working tree -(add)-> stage -(commit)->local Repository

working tree clean : 저장한 자료와 현재 모습과 일치하다.

git config : git 설치 이후 1번, 이메일 설정
git init : 설치 이후 특정 폴더를 git 으로 관리, 프로젝트당 1번
git add : stage 촬영시 마다
gid commit : local 저장
git checkout : 커서이동
git log
git status : 현재 상태 확인

Untracked files : 사진을 찍은 적이 없는 파일

add 취소법 : "git rm --cached <file>..." to unstage

git commit -m : -m가 없을 경우, 이상한 창이 열릴 것=> vi editor / 명령 프롬프트형 '메모장'
ㄴ> 키보드만 가지고 동작되는 프로그램
vi editor 1. command mode / 2. edit mode
ㄴ> 명령모드 : esc / 편집모드 : i(insert)

:wq => w(write) q(quit)

git gui : 디폴트 그래픽 유저 페이스
ㄴ repository(저장소) : commit 이력 쌓이는 곳 -> 어느 클라우드 공간(git hub 가능)
ㄴ visualize master's history

# 20231024
open git bash here : 깃 전용 탐색기
ㄴ> 사용용도 : 코드관리

리눅스 명령어

$ git status
ㄴ> 저장 현황 확인

$ git init
ㄴ> git 저장소 시작(초기설정)

$ touch memo.txt
ㄴ> 메모장 파일생성

$ ls
ㄴ> 현재 경로 내에 파일 확인

$ ls -l
ㄴ> ls 명령어에서 한줄씩 더 상세히 확인하는 법

$ ls -al
ㄴ> 숨김파일까지 확인

$ vi memo.txt
ㄴ> 파일 편집법

=====
edit mode : 단축키 i => 편집
command mode : 단축키 esc => 명령

:wq =>저장 후 빠져나오기

=====
$ cat memo.txt
ㄴ> 메모장 내에 정보 보기

$ git add .
ㄴ> 커밋(저장) 전에 대상 선택
ㄴ> .은 all 의미
ㄴ> *만약 경고문이 나온다면?
warning: in the working copy of 'memo.txt', LF will be replaced by CRLF the next time Git touches it
ㄴ> 내용에 확인되는 개행기호와 리눅스 개행기호는 서로 다른데 저장해도 되냐는 의미
ㄴ> 그냥 무시해도 좋음

$ git commit -m "memo.txt file added"
ㄴ> "내용" : 커밋 메시지 => 내가 어떻게 저장했는지 스스로 알아보기 위한 내용

===========
내용해석
$ git log
commit 582955e33edcfde8c828dddf80f8dea5d3acd9d8 (HEAD -> master)
Author: leeseungwoo <oy10302@naver.com>
Date:   Tue Oct 24 09:53:19 2023 +0900

    memo.txt file added
ㄴ> commit 582955e / commit id인데 너무 길어서 7자까지 id로 사용

===========
init 과정 정리
1. 임의의 폴더 안에 "open git bash here"를 실행하면 숨겨진 .git이 있음
2. 지웠다가 init하면 동일한 .git 파일이 생성이 되는데 최초 commit의 순간이다.
3. 최초 발생, 즉 기원은 바꿀 수 없다. 

===========

$ git branch lab1
ㄴ> branch : 포인터 생성
ㄴ> lab1는 포인터 이름 정의

$ git checkout lab1
ㄴ> 커서를 lab1로 옮기기

*내용을 수정했으면 꼭 commit 하기

==========
병합하기
: 임의의 포인터를 통해 성공적인 코드를 만들었을 경우 master과 합치는 과정을 말함

과정
1. 현재 커서(head)를 master로 옮기기
2. master 구간에서 병합 명령어

코드
1. $ git checkout master
2. $ git merge lab1

# 20231025

$ git log --graph
ㄴ> 가지 형태의 그래프(?)가 생성됨

*commit의 오해
: 모든 코드를 계속 저장하는 개념이 아니다.
최초 시점 기준으로 변경사항만 저장하는 개념이다.
용량도 적어지고 나뭇가지 형태로 데이터를 관리할 수 있다.

오늘 알아낸 것
1. 포인터 생성하고 내용 수정하든 내용 수정 후 포인터 생성하든 상관없고
add .과 commit만 잘하자.
2.  open git gui here 에 들어가 repository 누르고 visualize all branch history을 실행하면
모든 나뭇가지(graph)을 볼 수 있다.

# 20231026

branch 기능 사용전에 꼭 working tree clean 문구를 확인하라
ㄴ> 확인법: git status

$ git status
ㄴ> 저장 현황 확인

$ git diff
ㄴ> 저장 이후 바뀐 요소 상세설명

$ git gui &
ㄴ>git bash 별도로 gui 창을 활성화시킬 수 있음
ㄴ> 그래프 형태를 확인하고 싶을 때 보면 된다.

$ git commit
ㄴ> 기존에는 -m "(메시지)"로 기록을 남겼다면 그냥 commit은 여러줄의 메시지를 남길 수 있다.
ㄴ> 편집기가 활성화되면 사용법은 동일하다.
ㄴ> i는 편집, esc는 명령, 종료는 :wq

$ cd 주소창
ㄴ> 실행중인 git bash 위치 조정

==========
두 포인터의 충돌상황

$ git merge [포인터] 를 통해 나눠졌던 포인터를 결합하다가 충돌났을 경우
ㄴ> 에러메시지 : CONFLICT (content): ~
ㄴ> 대체방법 : 실제 코드파일 접속시 충돌 구간을 알리는 새로운 코드가 생성되어 있을 것임
ㄴ> 새로운 메시지 코드를 지우고 충돌 원인 코드를 수정하면 된다.
ㄴ> 그리고 add와 commit 진행

# 20231027

터미널 대신 window powershell 실행(
ㄴ> 파일탐색기 희망위치 내에 shift+마우스 오른쪽 키

git log 진행시 =>  (HEAD -> master, origin/master)
origin : 원격저장
ㄴ> 어제 gitHub 연결해서 저장하는 법 배움
ㄴ> 원격저장으로 'origin'으로 설정한 github.com/.... 형태의
내 계정 github 링크로 연결됨

개념정리
local Repository : 작업중인 현 컴퓨터 내부
Remote Repository : 원격저장으로 연결한 외부서버(github)

local에서 최초 작업 후 Remote로 업로드한 이후로 local에서 커밋하면?
ㄴ> Remote에선 최초 작업물까지만 가지고 있고 변화가 없다.

서로 다른 local 컴퓨터를 가지고 Remote에 있는 코드를 불러와서 
똑같이 수정 후 각 local 저장소에 commit하게 된다면 같은 master라고
할 수 있을까?
ㄴ> 같은 형태로 수정했더라도 엄연히 다른 코드라고 볼 수 있다.

한 사람은 local에서, 다른 한 사람은 Remote에서 똑같이 수정할 경우,
local에서 작업한 자가 Remote로 push(전달)하면 저장될까?
ㄴ> 안된다. 서로 다른 저장소에서 수정한 같은 단계의 master의 경우는
Remote에서 local 코드를 받아주지 않는다. 손상될 위험성을 방지하기 위함
ㄴ> 그럼 local의 입장에서 Remote로 push하려면?
ㄴ> local에서 Remote 코드를 다시 fetch(내려받기)한다. 
현 'origin/master' 포인터를 local에 가져와서 나뭇가지를 나눈다.
ㄴ> local에서 작업한 수정본(master)과 같은 단계에서 수정한
Remote(origin/master)를 merge로 결합한다. 충돌생기면 local에서 수정.
ㄴ> 그 상태에서 다시 결합한 master를 Remote로 push하면 된다.
ㄴ> Remote 내부에서는 local에서 merge한 코드를 받았을 것이다.

*푸시, 패치 과정에서 코드가 충돌나면 꼭 수정하고 주석으로 수정방식
작성하기, 협업시 알아볼 수 있도록 진행.
*git hub 입장에서 push받은 코드를 다른 컴퓨터로 옮길 때 '클론'이라 한다.

# 20231030

$ git remote -v(나열하다)

패치 후 머지하는 걸 '풀'이라 한다.

===
GitHub 업로드 이후 다른 컴퓨터에서 작업을 시도할 경우
1. 최초 기원은 이미 최초 컴퓨터로부터 만들어두었음, 그 상태로 깃허브
에 업로드되었으니 작업하고자 하는 다른 컴퓨터에 미리 git init을
할 필요는 없음, 아니 하면 안됨.
2. 깃허브 링크를 복사하고 작업하고자 하는 컴퓨터 내에 powerShell를 
키고 다음 문장을 붙어넣기
ㄴ git clone https://github.com/wooseung0124/MySecondRepo.git

# 20231031

예제준비

최초 local
ㄴ> C:\acorn202310\git_test

다른 local
ㄴ> C:\Users\acorn\Desktop\OtherCom

=======================
이전 수업의 전반적인 과정
1. local에서 최초 'git init' 생성(기원)
ㄴ> empty 저장소를 Remote 저장소로 등록

2. Remote(gitHub)
ㄴ> empty 저장소를 만든 다음
ㄴ> 기원 local에서 push 작업

3. 다른 local
ㄴ> Remote로 push했던 작업물을 가져와야한다.
ㄴ> 최초 다운을 'clone'이라고 한다.
==================
이번엔 github에서 기원을 설정하고 작업해보기

1.  GitHub에서 Create a new repository
ㄴ> Add a README file : 최초 init 설정

깃허브에서 나온 main은 master branch를 의미함

2. 링크 다운받고 'git clone (링크)'
ㄴ https://github.com/wooseung0124/MyTestRepo.git

3. github에서 다운 받은 파일을 local에서 작업 후 push할 때
ㄴ> $ git push origin main
ㄴ> main은 master branch에서 용어만 바뀐 것

4. github에서 수정한 코드를 다시 local에서 다운받을 경우
ㄴ> git pull


# 20231101

비주얼 스튜디오에도 git 기능 있음
ㄴ> git 이 설치되어있어야 됨
ㄴ> u : 추척되지 않은 파일이 있음
ㄴ> Changes 에 있는 + : add .
* 폴더 설정시 상위폴더 하위폴더 잘 구분하자.

lab1 branch 작업중에 이전 branch에서 수정할 게 생겼을 경우
ㄴ> lab1에서 작업했다고 착각하는 경우가 있음
ㄴ> 이 경우에는 lab1에서 커밋을 하지 않은 상황에서 커서를 이동시킴
ㄴ> lab1에서 수정했다고 볼 수 없기에 커서를 바꿔도 동일할 것임
ㄴ> 이상태로 main에 커밋하면 main 소속으로 데이터가 저장되니 주의

*임시저장 : git stash
ㄴ> 실행시 : 수정중인 코드가 눈에서 사라질 것임
*임시저장 불러오기 : git stash pop
ㄴ> 실행시  : 사라졌던 수정중인 코드가 다시 나타남
ㄴ> 저장파일 삭제하면서 가져오는 방식

git stash -u 
ㄴ> 저장하지 않은 파일은 해당하지 않기에 코드는 저장되더라도
새로 생성한 파일은 제외된다.
ㄴ> 때문에 이 명령어를 통해 수정과 추가된 모든 정보를 저장하는 
방법으로 진행하기 바람

git stash list
ㄴ> 임시저장 파일 존재여부 확인

git stash apply
ㄴ> 임시저장 리스트 정보 살린 상태로 불러오기

git stash drop (리스트 배열순서)
ㄴ> 임시저장 후 리스트 내에 데이터를 삭제를 원하는 경우
ㄴ> list 명령어를 통해 존재하는 파일을 조회하고 stash@{i}를 통해
  drop 명령어 뒤에 작성하면 삭제됨
*git Bash에서만 가능하며 파워쉘에선 동작안됨

# 20231102

만약 마지막 커밋 시점 이후로 일주일 동안 작업하다가 커밋하고나니
수정해야될 일부 코드가 확인됨, 이럴 경우는 어떻게 처리하면 좋을까
ㄴ> 커밋만 취소하고 일부 코드 수정 후 재커밋하면 됨

*그럼 수정이 필요한 코드를 커밋하고 깃허브로 바로 push하게 된다면??
ㄴ> 알아둘 것은 실수로 push한 경우는 수정코드로 재커밋해야함

커밋취소
$ git reset --hard HEAD~
ㄴ> --hard : 모두 없앤다(일주일치 데이터 없애기)
ㄴ> ~ : 개수에 따라 포인터를 뒤로 옮길 횟수를 말함
ㄴ> --hard (포인터)~ : 설정한 포인터 기준으로 1칸 뒤로 이동 후 이동한 만큼 제거
ㄴ> 결과 : working tree clean까지 없애기
ㄴ> 이전 포인터로 이동할 필요없이 현위치에서 수정한 코드만 수정을 원할 경우
: $ git reset --hard HEAD
ㄴ> ~ 만 안 적으면 그만임 / 근데 삭제취소는 안됨

커밋취소 복구
$ git reset ORIG_HEAD

모든 커밋 행적 확인
$ git reflog

변경사항을 남긴 채 커밋을 취소
$ git reset --mixed HEAD~
ㄴ> 대신 woking tree clean 기록 삭제됨

변경사항을 남긴 채 커밋을 취소
$ git reset --soft HEAD~
ㄴ> mixed와 차이점은 얜 woking tree clean 기록 남아있음

===========
만약 코드를 수정한 파일 외에 또다른 파일들이 많을 경우는?

$ git reset --mixed HEAD
ㄴ> 위에 방법으로 진행하면 코드에는 영향있으나 다른 파일들은 영향없음

$ git clean -fd
ㄴ> 이걸 실행하면 커밋 이후로 삭제를 희망하는 또 다른 파일도 삭제가능
ㄴ> 명심해야될 것은 영구적인 삭제이므로 주의하자.

# 20231103 

git 저장과정

working tree | -> | stage | -> | local Repo

	v1 -|-add-|-> v1 -|-commit-|-> v1

	v2 -|-add-|-> v2 -|-commit-|-> v2

local Repo 에서만 저장취소 : --soft
stage까지 취소할 경우 : --mixed
working tree 까지 취소할 경우 : --hard

===========================
개발하다가 처음부터 다시 코드하고 싶을 경우
ㄴ> 마지막 커밋으로 원상복구를 원할 경우
ㄴ> $ git reset --hard head
ㄴ> ~ 기호만 빼고 입력하면 됨

* 대신 코드 이 외에 또 다른 파일을 생성한 상태이고 그걸 지우고 싶다면??
ㄴ> $ git clean -fd
ㄴ> 커밋까지 존재했던 파일을 제외한 나머지 삭제
ㄴ> 이 과정은 영구삭제 과정임

# 20231106

상대방의 깃허브 자료를 내 깃허브 저장소로 가져올 수 있음
ㄴ > fork 라고 한다.
ㄴ > 이 작업의 장점 : 상대 깃허브에서 clone을 할 순 있어도 수정 후 push는
권한이 있지 않은 이상 불가함
ㄴ> 허나 상대 깃허브에서 나의 깃허브로 fork 작업하면 나의 저장소이기에
push작업 또한 가능하게 된다.

풀 리케스트(PR)
ㄴ> 상대 깃허브에서 다운 받은 코드를 나의 깃허브로 다운 받은 이후로 수정 및 실험한 이후 원본자께 marge 제안을 요청하는 과정

업스트림(상류 저장소)
ㄴ> 관례상 origin보다 높은 저장소(시초)
ㄴ> $ git remote add upstream (시초, 상대 깃허브 링크)
ㄴ> $ git remote -v : 확인법
ㄴ> $ git remote remove upstream : 취소법

과정
1. 상대 깃허브(시초) 에서 내 깃허브로 fork 작업
2. 내 컴퓨터 원하는 장소로 저장
ㄴ> git clone (내 깃허브 링크)
3. 내 깃허브에서 다운 받았지만 시초는 상대 링크이므로 최상위 정보 설정
ㄴ> $ git remote add upstream (fork했던 최초 깃허브 링크)

*만약 시초인 상대 깃허브(upstream)에서 수정이 진행되었을 경우
4. 다시 상대 깃허브 다운
ㄴ> $ git fetch upstream master
5. 나의 master(혹은 origin master)와 upstream master 병합
ㄴ> $ git merge upstream/master
6. 나의 깃허브 업로드
ㄴ> $ git push origin master




