평소에 R 만 쓰다보니 점점 지식이 편협해 지는 것 같아 Python을 해보려 마음먹었다.

나중에 까먹을 것이 분명하므로 일단 Mac에서 수치계산 및 기계학습을 실행할 수 있는 환경을 구축하는 순서를 정리한다.

이하 환경에서 정상 작동확인
OS X Yosemite (10.10.4)
설치 순서
Homebrew 설치
Ubuntu의 apt-get과 같이 Mac에서 패키지 관리를 편하게 해주는 Homebrew를 설치

`$ ruby -e "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/master/install)"`

Python의 버전 관리 툴 pyenv 설치
Python의 버전 2.xx과 3.xx의 사양은 큰 차이가 있다고 하나 자세한 것은 잘 모르므로 인터프리터 및 버전을 손쉽게 스위칭할 수 있도록 pyenv를 이용한다.

`$ brew install pyenv`

다음에 PATH를 설정

.bash_profile에 다음 설정을 추가

`export PATH="$HOME/.pyenv/shims:$PATH"`

Anaconda 설치
Anaconda는 Python의 수치계산환경을 구축하기 위한 여러 패키지를 모은 무료 배포판이다. Anaconda를 이용하면 NumPy, SciPy, matplotlib은 물론 기계학습라이브러리 scikit-learn등의 패키지도 설치할 수 있다.

다음 명령어로 설치가능한 Python 버전을 확인할 수 있다.

~~~
$ pyenv install -l
Available versions:

  2.1.3

  2.2.3

  ...

  anaconda3-2.2.0

  ...

  stackless-3.4.1
~~~
 
출력된 리스트 중 2015/07/19 현재 최신 버젼인 Anaconda(anaconda3-2.2.0)을 다음 명령어로 설치한다. 참고로 anaconda2_x.x.x은 Python 2 계열, anaconda2_x.x.x은 Pythone 3 계열을 의미한다.

~~~
$ pyenv install anaconda3-2.2.0
$ pyenv rehash
$ pyenv versions
* system
  anaconda3-2.2.0 (set by /Users/username/.python-version)
~~~

필수는 아니지만 pyenv-pip-rehash를 설치한다. pyenv으로 Python 환경을 스위칭할때 pyenv rehash를 자동으로 실행시켜 준다.

# pyenv를 Homebrew를 통해 설치한 경우
~~~
$ brew install homebrew/boneyard/pyenv-pip-rehash
# 기본 설정 상태
$ python --versions
Python 2.7.6
~~~
버전 스위칭
사용할 Python 설정
`$ pyenv global anaconda3-2.2.0`

현재 Python 버전 확인
`$ pyenv version
anaconda3-2.2.0 (set by /Users/username/.python-version)`

pyenv-pip-rehash를 설치하지 않은 경우에는
버전 스위칭 후 다음 명령어를 반드시 실행
`$ pyenv rehash`
Anaconda의 업데이트는 다음 명령어로 실행한다.

`$ conda update conda`
마지막으로 python을 실행하여 NumPy, SciPy, matplotlib의 테스트를 실행한다.

~~~
>>> import numpy
>>> numpy.test('full')
>>> import scipy
>>> scipy.test('full')
>>> import matplotlib
>>> matplotlib.test()
~~~

scikit-learn의 테스트는 bash에서

`$ nosetests --exe sklearn`

마지막에 다음과 같이 “OK” 메시지가 떨어지면 문제 없이 동작한다.

`OK (KNOWNFAIL=6, SKIP=8)`
