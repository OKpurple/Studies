- add (working dir -> Staging area(INDEX)
- commit (Staging area -> repository)
- push



Branch와 Merge

`$ git branch NewBranch` //'NewBranch'라는 새로운 브랜치 생성
`$ git checkout NewBranch` // 'NewBranch'로 옮겨감

위 2줄의 명령을 합쳐놓은 명령 : -b 옵션

~~~
$ git checkout -b NewBranch
Switched to a new branch 'NewBranch'
~~~

그리고 HEAD 브랜치는, 현재 작업중인 브랜치를 가리킨다.

- master branch(기본)
- NewBranch(현재 HEAD가 가리키는 브랜치) // 뭔가 일을 하고 커밋하면 이쪽에서 진행됨

갑자기 버그가 생겨서 바로 고쳐야 할시 NewBranch에서의 내용을 커밋해놓고
master branch로 checkout 한 후 버그를 고칠 FixBranch를 만들어 작업한다.
>git은 커밋한 내용을 자동으로 워킹디렉토리에 파일들을 수정, 삭제, 생성하여 checkout한 branch의 스냅샷으로 되돌려 놓음.

~~~
$ git checkout master
Switched to branch 'master'
$ git checkout -b FixBranch
Switched to branch 'FixBranch'
... [작업할 내용들]
~~~

문제를 제대로 고쳤는지 테스트 후 master branch에 합쳐야한다. (merge)

~~~
$ git checkout master
$ git merge FixBranch
Updating f42c576..3a0874c
Fast-forward
 README | 1 -
 1 file changed, 1 deletion(-)
~~~

Merge 메시지에서 'Fast-forward'가 보이는가? Merge할 브랜치가 가리키고 있던 커밋이 현 브랜치가 가리키는 것보다 '앞으로 진행한' 커밋이기 때문에 master 브랜치 포인터는 최신 커밋으로 이동한다.
> 단순히 master브랜치가 merge할 FixBranch의 커밋을 가리키고있음

문제를 급히 해결하고 master 브랜치에 적용하고 나면 다시 일하던 브랜치로 돌아가야 한다. 하지만, 그전에 필요없는 FixBranch 브랜치를 삭제한다. git branch 명령에 -d 옵션을 주고 브랜치를 삭제한다.

```
$ git branch -d FixBranch
Deleted branch FixBranch (was 3a0874c).
```

다시 NewBranch로 가서 작업을 진행해도 FixBranch에서의 작업내용은 일체 영향을 주지 않는다.


`git branch // show all branches`

`git reset HEAD // add 한 내용을 되돌립니다.` 
`git reset --hard HEAD // 모든 변경된 내용을 취소하고 마지막 커밋 상태로 복구합니다.` 
`git diff --cached // Index 와 local branch : last commit 간 차이점을 보여줍니다.`



[더 자세한 내용(참고사이트)] ("https://git-scm.com/book/ko/v1/Git-%EB%B8%8C%EB%9E%9C%EC%B9%98-%EB%B8%8C%EB%9E%9C%EC%B9%98%EC%99%80-Merge%EC%9D%98-%EA%B8%B0%EC%B4%88")

