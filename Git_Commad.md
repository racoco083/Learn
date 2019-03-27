### git 명령어 --help 
- 해당 명령어에 사용법을 알 수 있다.

### git log -p
- 전체commit의 소스코드 변화를 보여준다.

### git diff "commit1" "commit2"
- 공백을 사이로 첫 번째 commit과 두 번째 commit의 소스변화 등 차이를 보여준다.

### git reset "commit"
- reset뒤에 적어 준 coomit의 시간으로 작업이 백업된다. 사라진 버전은 사라진 게 아니라 존재 한다. git은 어떤 데이터도 버리지 않는다. 찾을려면 찾을 수 있다.
버전을 공유하고 나서는 절대 reset을 쓰면 안 된다. 왜냐하면 reset 후의 데이터와 다른사람이 공유한 데이터가 다르기 때문에 문제가 발생한다.

### git commit -am "11" 
- a는 add, m은 message로 뒤에 11이라는 메세지를 해당 커밋에 남긴다. 주의할 점은 git commit -a 를 할 때 한 번 도 add를 하지 않은 파일은 add가 되지 않는다.

※ Git objects 파일명의 원리
- http://milhouse93.tistory.com/4

※ Git commit 원리 
- https://opentutorials.org/course/2708/15240

### git branch exp (exp는 임의로 지은것이다. branch 특성에 맞게 naming하면 된다.)
- exp라는 branch를 만든다. 이 때 현재까지의 master에서 했던 commit들을 그대로 복사한다.

### git checkout exp
- exp branch로 이동한다.

### git checkout -b
- branch를 생성하고 생성한 branch로 전환까지 해준다. 

### git branch
- 모든 branch의 목록을 보여준다.

### git log --branches --decorate --graph --oneline
- 모든 branch의 log를 그래프적으로 정리해서 간결하게 보여준다.

### git log "비교할 브랜치 명 1" "비교할 브랜치 명 2"
- 브랜치 간에 비교할 때(소스코드 변화까지 보고 싶을 때는 옵션으로 -p를 주면 된다.)

### git diff "비교할 브랜치 명 1" "비교할 브랜치 명 2"
- 브랜치 간의 코드를 비교 할 때 

### A 브랜치로 B 브랜치를 병합할 때 (A ← B)
- git checkout A, git merge B

### git branch -d "삭제할 브랜치 이름"
- 사용 하지 않는 branch 지우기

### git branch -D "삭제할 브랜치 이름"
- "-d" 옵션으로 안되면 "-force"가 더해진 "-D"로 병합되지 않은 branch 강제로 지우면 된다.

### git reset --hard "commit" 
- 해당 commit 상태로 돌아가는 명령이다. 해당 commit 후의 commit들은 눈에 보지이 않지만
존재한다. 주의! 공유하는 것을 reset하면 안 된다.

※ git의 중복을 없애는 원리
- git은 파일의 이름이 달라도 내용이 같으면 같은 오브젝트 파일을 가리킵니다. 똑같은 내용의 어마어마한 중복의 내용을 없애준다. 내용이 같으면  blob id가 같다. 이걸 가능하게 하는 것은
SHA1의 해쉬 함수를 이용해서 내용에 따라 같은 blob id를 만들 수 있다.

git add f1.txt를 하면 이것이 blob이 된다.
commit, tree, blob 모두 외부에서 보기에는 큰 차이점이 없는 object 입니다.
구분이 되는 이유는 용도가 다르기 때문입니다.
간단하게 구분해 보면,
blob - 파일 하나의 내용을 보관
tree - blob 목록, tree 목록(포함 디렉터리, 없으면 제외) 보관
commit - parent(이전 commit, 이전 commit 없으면 제외), tree, author(코드 작성자), commit(코드 제출자) 보관

commit이 없는 branch는 git에서 아무리 많은 파일을 만들고 git add를 해도 없는
branch로 인식한다.

### rm "파일 이름"
- 파일 삭제

### rm -rf "디렉터리 이름"
- 디렉터리 삭제(-rf 옵션에 의해 하위디렉터리가 있어도 삭제한다.)

※ stach 정리
stash(감추다, 숨겨주다)

작업하고 있던 branch에서 작업이 끝나지 않았는데 다른 branch를 만들어 다른 작업도해야할 때 현 branch의 작업은 끝나지 않아 commit하기도 애매할 때 내가 작업했던 
내용을 어딘가에 숨겨 놓고 현 branch의 최근 commit으로 이동하게 해 준다. 그러면 branch를 새로 만들 때 현 branch의 작업을 그대로 복사하는데 git stash를 해 주면
현 branch의 최근 commit으로 이동하게 되고 그 후의 작업은 숨겨지고 새로운 branch를 만들면 최근 commit까지만 복사한다. 그리고 현 branch에서 숨겨둔 작업을 불러오려면
git stash apply를 해 주면 된다. stash의 list들을 명시적으로 지워주지 않으면 apply를 통해 언제든 다시 불러 올 수 있다.

stash를 하면 untracked작업은 list에 올라가지 않고 무시한다. untracked 작업은 따로 처리 해 주어야 한다.  


### git stash list
- stash를 사용해 숨겨 둔 작업을 확인 할 수 있다.

### git reset --hard (HEAD)
- 현 branch의 가장 최신 commit 이후의 내용들을 다 지운다.

### git stash apply
- 스택처럼 apply를 하면 stash list에서 최근 작업을 하나씩 불러온다. 

### git stash drop
- stash list에서 가장 최근에 숨긴 작업을 지운다. 인덱스 0인 작업은 삭제되고, 인덱스 1인 작업은 인덱스가 0으로 바뀐다.stash list는 인덱스가 작을수록 최근에 숨겨진 작업이며 

### git stash pop 
- git stash apply하고 git stash drop을 해주는 명령어

### 원격 저장소를 추가한다.
git remote add origin https://github.com/racoco083/"repository name"
https://github.com/racoco083/"repository name"이것은 기니까 origin으로 대체한다. 이름이 기니까 별명으로 대체한다고 생각하면 된다. origin대신 다른 별명을 써도 된다.

### git remote remove origin
- 원격 저장소 origin을 삭제한다.

### git push --set-upstream origin master
- 원격저장소 origin의 master branch로 local의 현 branch의 작업들 업로드한다. (--set-upstream == -u) 한 번 이 명령어로 수행한 후에는 연결이 되어 다음부터는 git push만 해도 된다.

### git remote -v
- 모든 원격저장소 확인

local저장소에 작업한 것을 원격저장소에 업로드 한다. 이걸 한 후에 항상 유저이름과 이메일을 물어본다. 이걸 방지하기 위해
git config --global user.name "racoco083"
git config --global user.email uytr083@naver.com
이 두 명령을 해 주면 물어보지 않는다. 이건 git 쓰면서 맨 처음 한 번만 하면 되는 명령어들이다.

### git clone http://github.com/git/git.git gitsrc
- 현 폴더에서 gitsrc폴더를 만들고 http://github.com/git/git.git(저장소)모든 내용을 복사해서 gitsrc에 저장한다. 현재 디렉터리에 저장하고 싶으면git clone http://github.com/git/git.git . 해주면 된다.

### git log --reverse
- 거꾸로 git의 log를 볼 수 있다.

### git checkout "commit id"
- branch처럼 commit도 checkout 할 수 있다. checkout후 git log를 하게 되면 해당 commit부터 과거의 모든 commit을 볼 수 있다. 그리고 이 상태에서 ls -al 하면 그 commit시점의 파일 상태를 확인 할 수 있다..

### git commit --amend
- 가장 최근 commit의 내용을 수정할 수 있다.

### git tag "태그의 이름" "commit" or "브랜치 이름"
-master는 항상 가장 최근의 commit을 가리킨다. 브랜치 이름에 master를 넣으면 가장 최근의 커밋에 태그가 붙는다.
ex) git tag 1.0.0. master

주석을 추가하는 태그이다.
옵션 -a는 annotated 주석을 쓰기 위해서 사용한다.
옵션 -m은 주석을 단다.
git tag -a 1.1.0. -m "bug fix"

### git tag -v "태그의 이름"
- 해당 태그의 자세한 내용이 나온다.

### git push --tags
- 원격저장소에 local에서 만든 태그를 원격저장소에 올린다. release가 태그를 가리킨다.

### git tag
- 태그의 목록을 보여준다.

### git rm -r filename
- add된 파일을 지운다.

### git tag -d "태그이름"
- 특정 태그를 지운다.

### git rebase master
- master와 exp branch가 있다고 한다면 exp branch에서 git rebase master를 하면 exp의 뿌리 커밋을 master가 가리키고 있는 커밋으로 바꾸겠다는 뜻이다.

충돌부분 </br>
// <<<<<<< HEAD </br>
// commit: 인덱스의 상태를 기록하기 </br>
// ======= </br>
// pull: 원격 저장소의 내용을 가져오기 </br>
// >>>>>>> exp </br>

rebase 의 경우 충돌 부분을 수정 한 후에는 commit 이 
아니라 rebase 명령에 --continue 옵션을 지정하여 실행해야 한다.
git rebase --continue

### git rebase -i HEAD~3 (숫자는 최근 커밋부터 과거 커밋까지의 개수를 나타낸다.)
현재 HEAD가 가리키고 있는 커밋부터 과거 두개의 커밋까지의 목록을 보여준다.
목록에 pick이나 squash, reword에 대한 설명이 있으니 참고하자!

※ git issue 협업에 대해 잘 설명해 놓은 동영상

https://www.youtube.com/watch?v=YshvUGgF_3o

※ 소스코드에서 blame을 클릭한 뒤 왼쪽 특정 commit을 클릭하면 밑의 화면이 나온다. 협업시 코드에 comment를 달 수 있다.

![image](https://user-images.githubusercontent.com/21019088/50052413-0776db80-0167-11e9-8491-7742414ea07a.png)

## :star: git push origin develop(branch) 
이런식으로 하면 원격저장소에 commit한 것들이 update 되지 않는다.
master branch에 merge한 후 git push origin master를 해야 update가 된다.

