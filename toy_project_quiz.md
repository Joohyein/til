# 6일차

토이 프로젝트에 issue를 추가하고 해결해보는 시간을 가졌다. 시간이 부족해서 넣지 못했던 기능과 버그를 수정하는 issue를 추가해보았다. issue가 많았지만 그 중에서 내가 해결한 issue는 쉬운 것들이었다.

- 이슈 목록
    - input창 비우기 : 문제를 틀렸을 때 input안에 있는 문자들을 지우기
    - 문제 풀기 오답기능 업데이트 : 틀렸을 때 alert창을 띄웠는데 input창 오른쪽 끝에 '오답입니다'를 띄웠다.

sourcetree에서 pull을 했을 때 오류가 떠서 풀을 하지 못했다.   

    <오류코드>
    * branch main -> FETCH_HEAD hint: You have divergent branches and need to specify how to reconcile them. hint: You can do so by running one of the following commands sometime before hint: your next pull: hint: hint: git config pull.rebase false # merge hint: git config pull.rebase true # rebase hint: git config pull.ff only # fast-forward only hint: hint: You can replace "git config" with "git config --global" to set a default hint: preference for all repositories. You can also pass --rebase, --no-rebase, hint: or --ff-only on the command line to override the configured default per hint: invocation. fatal: Need to specify how to reconcile divergent branches.


#### 해결
기본 mode 같은 경우, git pull 을 수행하게 되면 git merge commit 을 생성하게 됩니다. 따라서, 기존에 존재하지 않는 commit 이 자동으로 생기게 된다. pull 을 받을 때 마다 불필요한 merge commit 이 생기게 되는 것이다.

1. git config pull.rebase false #merge (the default strategy)
2. git config pull.rebase true #rebase
3. git config pull.ff only # fast-forward only   
- true : rebase 활성화

- 2 -> git pull 의 default 옵션으로 지정되어 옵션이 주어져 실행됩니다.

- 3 -> git pull --ff-only 를 기본 정책으로 가져갈 경우 매번 입력해야되는 번거로움이 존재한다. 또한, 만약 실수로 빼먹고 작업을 하게되면 history 가 꼬이는 상황이 발생할 수 있기 때문에 기본설정이 필요한 경우가 있습니다.


### 알게 된 점
rebase는 원본을 바꾸는 행동 중 하나이다. 기존의 로그를 덮어씌워서 히스토리가 사라짐. 방법론을 잘 지키면 rebase를 사용할 일이 없다. config 설정을 바꿔주는 명령어이다. rebase를 true가 default이다. 


*** 


### 오늘 알게 된 css 

    - 애니매이션 유지하기
    animation-fill-mode: forwards;

    - '오답입니다' 텍스트가 답을 여러 번 입력했을 때 reload가 되는 것을 보여주기 위해 0% ~ 5%까지 텍스트의 크기의 변화를 줬다.
    @keyframes fadeout {
        0% {
            opacity: 1;
            font-size: 20px;
        }
        5% {
            font-size: 16px;
        }
        95% {
            opacity: 1;
        }
        100% {
            opacity: 0;
        }
    }


    




    



