# NVM(Node.js Version Manager)

###기대효과
>기존의 nvm을 사용하지 않고 설치한 노드는 /usr/local/bin에 설치가 되어 관리자 권한 없이는 제대로 실행이 안됨. 특히 -g 옵션을 줘서 global로 모듈을 설치할 때 마다 sudo 해줘야 하는 불편함이 없다.


- install

`$ curl https://raw.githubusercontent.com/creationix/nvm/v0.13.0/install.sh | bash`

- install 과정 진행 후 $HOME에 .nvm 디렉토리 생성.
- 자동으로 __/$HOME/.bash\_profile (mac)__, __/$Home/.bashrc (linux)__에 아래 환경변수 내용 추가가 됩니다.

~~~
export NVM_DIR="$HOME/.nvm"
[ -s "$NVM_DIR/nvm.sh" ] && . "$NVM_DIR/nvm.sh"
~~~
- 터미널을 재실행하면 nvm 명령어가 사용가능합니다.

~~~
$ nvm ls-remote // 설치가능한 node.js 버젼
$ nvm ls	// 설치된 node.js 버전들의 리스트
$ nvm install node //최신버전의 node를 인스톨
$ which node // node가 설치된 위치
~~~
- __$HOME/.nvm/versions__에 설치된 버전별로 디렉토리가 만들어져 있음
- 하지만 이렇게 설치를 했다고 해도 터미널을 새로 열어서 node.js 명령을 실행하면 시행이 안되는 것을 볼 수 있습니다. 그건 매번 터미널을 새로 실행하게 되면 nvm 환경설정이 초기화 되어서 그런것인데 다음과 같은 명령으로 활성화가 가능합니다.

~~~
$ nvm use [version] //ex) nvm use v7.7.1
$ 
$ nvm use v7.7.1
$ node -v //노드 버전 확인
$ v7.7.1
~~~
- default로 alias를 걸면 매번 활성화 시켜줄 필요가 없어짐

~~~
$ nvm alias default 7.7.1
$ nvm list
->       v7.7.1
default -> 7.7.1 (-> v7.7.1)
node -> stable (-> v7.7.1) (default)
stable -> 7.7 (-> v7.7.1) (default)
iojs -> N/A (default)
~~~

-  npm 으로 여러 라이브러리를 설치해도 __$HOME/.nvm/[version]__ 디렉토리에 격리되어서 설치가 되어서 라이브러리가 꼬여 발생하는 문제도 없을뿐더러 초기화 하는 방법도 간단합니다. __$HOME/.nvm__ 디렉토리를 그냥 삭제만 해주면 됩니다.