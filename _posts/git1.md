---
layout: post
title:  "git -1편"
excerpt: "git을 공부해보자"

tags:
  - [Blog, jekyll, Github, Python]

toc: true
toc_sticky: true
 
date: 2023-03-09
last_modified_at: 2023-03-09
---
{% include toc.html %}

### 1. git,그리고 github
깃(git)에 대해서 정리를 해보려고 시작한다.
git을 막연하게 주먹구구식으로 사용하고 있었는데, 이를 좀 더 편리하고 정확히 어떤게 무엇인지를 판단해야한다고 생각되었다.
지금까지는 협업이 적어서 괜찮다고 생각했는데, 같이 연구하는 친구랑도 항상 깃허브를 들어가서 불편하게 진행했는데
이번 기회에 좀 더 정확하고 편리하게 사용하기 위하여 공부해본다.

우선 버전관리에 대해서 알아보자.
버전관리는 간단하게 말하면 내가 원하는 시점으로 이동할 수 있게 하는 것이 버전관리이며 이를 도와주는 툴이 버전관리 시스템이다.
이러한 툴이 혼자서 사용할 때는 그냥 진행하면 되지만, 인원이 많아질 수록 어떤 것이 최종 업데이트 파일인지 파악하는 것이 힘들다.

그래서 나타난 툴이 git, github라는 툴이다.
github, gitlab, bitbutcket 이 존재하며 각자 다른 특성을 가지고 있다.
github와 gitlab이 같은 라인인 줄 알았는데 다른 회사라는 것을 알게되었다.

우선은 사용법을 정확하게 익히기 위하여 다른사람과 협업이 아닌 혼자서 버전관리를 한다는 마음으로 진행하도록 한다.

### 2. 내 컴퓨터에 git 설치하기

우선 내 컴퓨터의 환경은 ubuntu 22.04이다. 그래서 우분투 방식으로 install하기로 했다.

{%highlight css%}
sudo apt-get install git
git --verison
{%endhighlight%}
을 하여서 설치 후, 잘 설치가 되었는지 확인한다.
설치했을 때 git version 2.34.1이 설치되어있음을 확인할 수 있었다.

윈도우의 경우 git bash를 설치해야지 사용할 수 있는데, 우분투나 맥의 경우 그냥 git만 설치하여도 터미널에서 사용할 수 있다는 장점이 있다.

### 3. 로컬 저장소 만들기
이제 내 컴퓨터에서 설치한 git과 연결할 로컬 저장소를 만들어 보자 로컬저장소는 실제로 git을 통해 버전관리가 이루어질 내 컴퓨터에 있는 폴더이다.
나는 Desktop/바탕화면 에 gitpractice라는 폴더를 만들었고 이를 실습에 이용할 예정이다.

우선 readme.txt라는 파일을 생성해주자
이번에 git 공부를 하면서 리눅스 명령어와 친해지는 시간을 가지도록 할 것이다.
{%highlight css%}
touch readme.txt
{%endhighlight%}
명령어를 입력하면 파일이 생성된다.
그런다음, 해당 폴더 위치에서 터미널에
{%highlight css%}
git init
{%endhighlight%}
을 이용하여 git을 시작해주도록 하자
Initialized empty Git repository in /home/hyunskki/바탕화면/gitpractice/.git/
이런 메세지가 출력되면서 git이 시작되었음을 알 수 있다. 또한 폴더에 자동으로 .git이 생성된 것을 확인할 수 있다.
이 폴더에는 git으로 생성한 버전들의 정보와 원격저장소 주소등이 들어있고 이를 로컬 저장소라고 부른다

#### git init : Git 초기화 과정(로컬저장소 생성)

### 4. 첫번째 커밋 만들기
방금생성했던 readme.txt파일을 하나의 버전으로 만들어보자. git 에서는 이렇게 생성된 버전을 commit이라고 부른다.
생성하기 전 해야할 일들이 있다.
먼저 버전관리를 위하여 내 정보를 등록해야한다. 각 버전을 누가 만들었는지 알아야하기 때문이다.

{%highlight css%}
git config --global user.email "gustjr7879@naver.com"
git config --global user.name "hyunskki"
{%endhighlight%}
이렇게 하면 버전관리하는 사람의 정보를 등록할 수 있다.

다음으로 커밋에 추가할 파일을 선택한다. 조금 전 만들어 놓은 readme.txt파일로 해보자
{%highlight css%}
git add readme.txt
{%endhighlight%}
커밋에는 상세 설명을 적을 수 있다. 설명을 잘 적어 놓으면 내가 이 파일을 왜, 어떤것때문에 수정했는지를 파악할 수 있다.

{%highlight css%}
git commit -m "실습 진행중"
{%endhighlight%}
을 입력해서 commit 메세지를 추가했다.
1 file changed, 메세지가 출력되면 성공이다.

이렇게 버전을 하나 생성하고, 다른 버전을 만들어보자

{%highlight css%}
nano readme.txt
{%endhighlight%}
를 입력하여 아무 글자나 적어놓도록하자

그런다음 위의 과정과 같이 add 를 통하여 파일을 선택하고 "내용 변경 버전" 이라는 메세지와 함께 commit해보자

### 5. 다른 커밋으로 시간 여행하기

위와 같이 만들어둔 커밋으로 언제든지 시간여행을 할 수 있다.
개발을 하다가 요구사항이나, 변경사항이 발생 시 이전 커밋부터 해야겠다 싶으면 git을 사용하여 그 커밋으로 돌아갈 수 있다.

현재 readme.txt파일의 내용은 업데이트를 한번 진행한 커밋이다. 이걸 첫번째 만들었던 커밋 버전으로 되돌려보자.

{%highlight css%}
git log
{%endhighlight%}
를 입력하게 되면 가장 위에 있는 내용이 최근에 commit한 내용이다.
commit 823ace3....
commit 57d6b99... 같이 나와있을건데 이를 잘 확인 후 되돌리고 싶은 커밋 앞 7자리 커밋 아이디를 복사하고 checkout 명령어로
해당 커밋으로 코드를 되돌린다. 지정한 커밋아이디를 입력해야한다.
마지막에 HEAD is now at ,,, 메세지가 나온다면 커밋을 되돌린것이다.
{%highlight css%}
git checkout 57d6b99
{%endhighlight%}
그러면 다시 수정된 커밋으로 되돌아가보자
다시 커밋아이디를 입력해서 되돌아갈 수 있고, 아니면
{%highlight css%}
git checkout -
{%endhighlight%}
로 되돌릴 수 있다.

### 6. github 원격저장소에 커밋 올리기
위의 내용은 내 컴퓨터에서 나 혼자만 버전을 관리할 수 있다. 하지만 github에 올려서 다른 개발자들과 함께 버전관리를 하려면 원격저장소에 올려야한다.
github에서는 원격저장소를 레포지트리(repository)라고 한다. 
내 깃허브에서 레포지트리는 gitpractice로 만들었다. 여기에서 레포지트리 주소를 복사한다.

이제 github에서 만든 gitpractice 레포지트리 주소를 내 컴퓨터의 로컬저장소에 알려주고, 로컬저장소에서 만들었던 커밋들을 레포지트리에 올려보자.
{%highlight css%}
git remote add origin https://github.com/gustjr7879/gitpractice.git
{%endhighlight%}
를 입력하게 된다면 주소를 알려준 것이다.

이제 로컬저장소에 있는 커밋들을 push 명령어로 레포지트리로 옮겨보자. 여러 생소한 명령어는 나중에 설명하도록하고,
{%highlight css%}
git push origin master
{%endhighlight%}
이때 user naem과 user password를 입력하라고 하는데, 제대로 입력해도 안되는 경우가 있다.
이때는 github에서 발행한 토큰을 패스워드에 입력해주면 로그인이 된다. (이유는 잘,,)
%진행도가 보여지면서 push가 종료되었고, 레포지트리에 가보면 branch가 2개가 되어있다. 
즉 main branch : 생성하면서 만들어진 branch
new branch : 방금 push로 생성한 branch이다.
새로운 branch를 main branch에 병합해야한다. 브랜치 병합은 merge로 사용한다.
merge에 대한 내용은 후에 나오는 내용으로 나중에 공부하자 !

### 7. github 원격저장소의 커밋을 로컬 저장소에 내려받기
방금은 로컬 저장소에서 레포지토리로 올려봤다면 이번에는 레포지토리에서 로컬저장소로 내려받는 것을 해볼 것이다.

레포지토리의 코드와 버전 전체를 내 컴퓨터로 내려받는 것을 clone(클론)이라고 한다. 클론을 하면 최신 버전 뿐만 아니라, 이전 버전들과 원격저장소 주소등이 내 컴퓨터의 로컬 저장소에 저장된다.

먼저 새로운 폴더를 만들어준다 -> 이 폴더는 원격저장소에 올린 커밋을 내려받는데 사용된다.

{%highlight css%}
mkdir subfolder
{%endhighlight%}
그리고 원격저장소 주소를 입력하면 어떠한 원격저장소던지 로컬 컴퓨터로 내려받을 수 있다. 

{%highlight css%}
git clone https://github.com/gustjr7879/gitpractice.git
{%endhighlight%}
를 입력해주면 내 로컬 컴퓨터로 다운로드가 진행된다. 물론 그 전에 다운로드 받을 폴더로 이동해주어야 한다.
퍼센트가 뜨면 정상적으로 진행되었다는 뜻.

하지만 폴더에 폴더가 생성되어서 보기 싫을 수 있다.
이럴때는

{%highlight css%}
git clone https://github.com/gustjr7879/gitpractice.git .
{%endhighlight%}
똑같이 한 다음에 맨 뒤에서 한칸 띄고 .을 찍어주면 해결할 수 있다.
그렇게 하면 레포지토리가 폴더안에서 작동한다. 이때 
{%highlight css%}
git checkout master
git checkout main 
{%endhighlight%}
을 하게 된다면 master와 main branch를 왔다갔다할 수 있게된다.

{%highlight css%}
cat readme.txt
nano readme.txt
{%endhighlight%}
를 통하여 readme.txt파일을 바꿔줘보자
그런 다음에
{%highlight css%}
git add readme.txt
git commit -m "2차 실습 진행"
git push origin master
{%endhighlight%}
를 하면 레포지토리에 push할 수 있게된다.

위의 방법대로하면 subfolder에 있는 readme.txt 파일은 갱신되어있지만, gitpractice 에 있는 파일은 갱신되어있지 않다.

원격저장소의 새로운 커밋을 로컬저장소에 갱신하는 방법은 
{%highlight css%}
git pull origin master
{%endhighlight%}
를 입력하면 readme.txt 파일이 변해있는 것을 확인할 수 있다.
pull 명령어는 레포지토리에 새로운 커밋이 있다면, 그걸 내 로컬 저장소에 받아오라는 명령어이다.
