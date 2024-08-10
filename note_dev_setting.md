# MLOps 용 linux 환경 셋팅하기
- MLOps 를 실행하려면 kubernetes와 관련된 다양한 오픈소스들을 동시에 사용해야하므로 linux 환경에서 작업한다.
- 따라서 window 환경이든 mac 환경이든 linux를 사용하기 위한 방법으로 Virtual Box를 통해 가상의 컴퓨터 머신(VM)을 설치한 후 이곳에 Ubuntu를 설치한다.
- 기존 컴퓨터의 자원을 VM과 분리해서 사용해야 하므로 메모리, 용량 관리를 해주어야 한다.
- 특히 MLOps의 여러 오픈소스들을 실행하려면 VM의 성능이 일정수준 이상이어야하는데, 기존 컴퓨터의 자원이 그만큼 넉넉해야 한다.

## 1. VM Ubuntu 설치
- virtual box -> vm -> ubuntu

### 1) Virtual Box 설치
- www.virtualbox.org/wiki/Downloads 에서 OS 환경에 맞는 설치 패키지 다운로드
- 설치 하면 VM을 구성하는 여러가지 단계들을 거치게 된다.
   - **VM을 만들 때 ISO image를 Ubuntu 압축파일을 직접 선택해야 실행이 잘 된다.**
   - ISO image를 따로 지정해주지 않으면 vm과 ubuntu가 한 곳에 설치 되지 않는 것 같다.
- VM 자원 셋팅
   - ISO image : ubuntu-22.04.3-desktop-amd6
   - 메모리 12gb 
   - cpu 6
   - 용량 80gb
   - name : vmkuber
   - username : 
   - pw : 

### 2) Ubuntu 다운로드
- www.ubuntu.com/downloads/desktop 에서 최신버전 혹은 원하는 버전의 ubuntu 설치파일 다운로드

### 3) vm 만들 때 ubuntu 파일 선택
- vm이 생성되면서 os로 ubuntu를 설치한다.

### 4) 기타 셋팅
- vm 을 셋팅하면서 언어, 키보드 유형 등을 선택한다.
- vm 의 정보 입력
   - 컴퓨터 이름과 비번은 ubuntu 실행시 입력하는 정보이므로 따로 저장한다.

## 2. linux 셋팅
- vm(가상머신) 생성이 끝난 후 실행하면 ubuntu가 실행된다.
   - 윈도우 처럼 컴퓨터의 os로 ubuntu를 사용
   - vm 생성할 때 설정한 비번 입력
- ubuntu는 linux 체제 이므로 terminal을 사용할 수 있다.
- 개발은 vscode 등의 IDE를 설치하여 사용한다.

### 1) sudo 권한 설정
- su : root 계정으로 전환, root 계정의 암호 입력 필요
- sudo : 계정 전환 없이, 일시적으로 root 권한을 부여하는 방식, 사용자 계정의 암호 입력 필요
- sudo 명령어가 적용되지 않을 경우 sudoers 파일에서 사용자를 등록(추가) 해준다.
  - su 입력하여 root 계정으로 변환
  - ls -al | grep sudoers 입력하여 확인
  - visudo -f /etc/sudoers 입력하여 sudoers 파일 열기
  - #User privilege specification 항목 아래에 root ALL=(ALL:ALL) ALL 한 줄 밑에 hsh ALL=(ALL:ALL) ALL 입력 후 저장
  - exit 입력하여 root 계정 종료
  - hsh 계정에서 sudo 명령어 입력하면 사용가능

#### 암호 생성
- 명령어 입력하면 암호를 설정할 수 있다.
```
$ sudo password
```

## 3. 개발용 가상환경 설정
- 가상환경을 만들어 패키지 버전 관리를 효율적으로 한다.
- 가상환경 종류 2가지
   - venv : python의 가상환경
   - conda env : 아나콘다의 가상환경
- 이 중 어떤것으로 가상환경을 만들고 상요해도 된다. 하지만 아나콘다의 가상환경을 사용하는 것이 패키지의 버전관리를 하는 데 더 유용하다.

### 1) Anaconda env
- 파이썬 패키지 매니저 + 개발환경 매니저 기능이 들어 있음
   - pip + venv의 기능
- venv는 python3에 포함되어 있는 가상환경 기능
- 콘다는 아나콘다의 툴
   - 아나콘다는 데이터 사이언스 용 패키지들이 들어있어서 용량이 큰 편
   - 간단하게 사용할 때는 miniconda를 사용해서 패키지 매니저 + 개발환경 매니저를 사용해도 됨
- 대부분의 개발은 가상환경에서 이루어진다.
   - 프로젝트 마다 사용하는 패키지의 버전이 다른 경우가 많기때문

#### 아나콘다 설치
- 우분투나 윈도우에서 아나콘다(또는 미니콘다)를 설치해서 사용
   - anaconda 또는 미니콘다 설치 스크립트 url 주소 복사 ===> wget <url 주소> ===> 다운로드 (.sh 파일) ===> 콘다가 설치될 디렉토리로 파일 이동 ===> 설치 (bash ./Miniconda~.sh) ===> 설치 완료 되면 conda list 로 설치 결과 확인
   - conda list : 아나콘다 패키지 리스트
   - conda --version : 아나콘다 설치 후 버전 확인

#### 아나콘다 가상환경 설정
- 가상환경 생성 
   - python 버전을 설정해주면 해당 버전의 python이 설치 된다
```
$ conda create --name 가상환경이름 python=3.8
```

- 가상환경 활성화
```
$ conda activate 가상환경이름
```

- 가상환경 비활성화 
```
$ conda deactivate
```

- 가상환경 리스트 
```
$ conda env list
```

- conda 가상환경 삭제
```
$ conda remove --name <가상환경 이름> --all
```

- conda env list 
```
$ 가상환경 확인 
```
#### conda 가상환경 yaml 파일로 export
- 활성화 된 conda 가상환경의 환경을 yaml 파일로 내보내고, yaml 파일로 가상환경을 설치할 수 있다.
   - 중요한 conda 가상환경은 .yaml 파일로 export 해서 관리하는 것도 좋을 것 같다.
```
$ conda env export > environment.ymal
```

- yaml 파일로 conda 가상 환경 패키지 설치
```
(가상환경이 활성화 되어 있는 경우)
$ conda env update --file environment.yaml 

(가상환경이 비활성화 인 경우)
( --name에 해당하는 가상환경이 없는 경우에 실행하면 --name으로 가상환경을 만들고 .ymal. 파일의 package들을 설치한다.)
$ conda env update --name <env name> --file environment.yaml 
```

### 2) python 가상환경 venv
- python 자체 가상환경 venv
   - venv는 파이썬 표준 라이브러리에 내장 되어 있음
   - 따로 설치 필요 없음
   - 가상환경 디렉토리의 pyvenv.cfg 를 보면 python 버전이 ~/anaconda3 와 연동되는 것을 알 수 있다.
   - python -m venv 가상환경 이름 ===> 가성환경 생성
   - 가상환경 이름의 디렉토리가 생성 되고 이 안에 여러가지 파일이 있음
   - 가상환경 활성화 : source ./bin/activate
   - 가상환경 비활성화 : deactivate
   - 가상환경 활성화후 conda list 확인 하면 venv 가상환경 디렉토리와 anaconda3 디렉토리의 설치내용이 같다.
   - pip list는 다를 수 있다. venv 가상환경에서 필요한 설치 파일들을 다르게 설치 했을 수 있으므로..
   - 가상환경 삭제 : sudo rm -rf 가상환경 이름

### 3) 가상환경에서 패키지 설치
- 가상환경에서 특정한 패키지를 설치하려면 pip install 또는 conda install 을 사용한다.
- pip 로 설치 한 것은 pip uninstall로 삭제 하고, conda install로 설치한 것은 conda uninstall로 삭제한다.
- pip list와 conda list가 다를 수 있다.
   - 거의 같다.
   - 패키지의 용어가 다를 수 있으므로 grep 을 사용해서 검색할 경우 이 점을 확인 할 것

#### pip 업데이트
```
$ python -m pip install --upgrade pip 
```
#### apt 업데이트
- apt는 ubuntu에서 사용하여 패키지 관리 프로그램
```
$ sudo apt-get update
$ sudo apt update
```
#### git 설치
   - sudo apt update ===> sudo apt install giㅅ ===> git --version 확인
   - git은 코드의 버전관리 시스템
   - tig 설치 : git 커밋 히스토리를 터미널에서 보여주는 툴
      - sudo apt install tig

#### requirement 파일로 패키지 설치
- 개발용 가상환경에 설치 된 여러 패키지 리스트를 텍스트 파일로 만든 후 한번에 설치할 수 있다.
- 현재 pip 설치 내용을 텍스트로 저장
```
$ pip freeze > req.text
```

- req.text 한번에 설치
```
$ pip install -r req.text
```

- req.text 한번에 삭제
   - 단, 한번에 삭제하면 가상환경 구성 파일들도 모두 지워지므로 다시 아나콘다를 설정해야할 수 도 있다.
```
$ pip uninstall -r req.text -y
```

#### req.text 패키지 설치 시 불필요한 문자열 제거해야한다.
- vim에서 req.text 의 불필요한 문자열을 제거한다.
- :%s/<원하는 문자열 입력, 빈공간 가능>.* /<대체할 문자열, 빈공간 가능>/
   - 모든 행에서 email 다음의 모든 문자열을 한번에 지워준다.
   - <> 과 <> 다음에 오는 모든 문자열 선택 <>.*
   - <>... : .하나가 다음 문자열 1개를 선택해준다.
   - <>.* 을 // 이것을 replace 한다. 즉 비어있는 값으로 바꿔준다.
   - %s/file/apple/ ---> file을 apple로 replace 한다.
   - %s/file../apple/ ---> file 다음 .. 2개 문자열까지 선택한 후 apple로 replace 한다.
      - file@@@ 인경우 2번째 @까지 선택됨

## 4. 유용한 명령어들

### 1) linux 메모리 확인
- sudo su : root 계정으로 전환 (pw 입력)
- 메모리 정리
   - echo 3 > /proc/sys/vm/drop_caches
   - caches 정리
- free -h : 메모리 사용 현황 GB로 요약
- free -m : 메모리 사용 현황 MB로 요약
- top : 윈도우의 작업관리자 같은 summary : 실시간 메모리 사용 현황

### 2) grep

#### 기본 방식
- grep "<문자열>" <파일명>
   - grep "pytest" unit_test.py : unit_test.py에서 pytest 문자열 찾기
   - grep "pytest" *.py : .py 확장자를 가진 모든 파일에서 pytest 문자열 검색
- -r : 현재 디렉토리 내에서 모두 검색
   - grep -r "pytest" * : 현재 디렉토리내의 모든 파일 (*)에서 pytest 문자열을 검색
- -H : 파일명 표시
   - grep -r "pytest" * -H : 현재 디렉토리내의 모든 파일에서 pytest 문자열을 검색하고 파일명을 함께 출력
- -n : 문장의 번호 출력
   - grep -r "pytest" * -H -n : 현재 디렉토리내의 모든 파일에서 pytest 문자열을 검색하고 파일명과 문장의 번호를 출력
- "a.*b" : a로 시작하고 b로 끝나는 문자열 검색      
   - grep "a.*e" app.py : app.py 파일에서 a로 시작하고 e로 끝나는 문자열을 검색
- "^context" : context 로 시작하는 문장 검색   
   - grep "^Context" help.text : help.text 파일에서 Context로 시작하는 문장 검색
- "apple.$" : apple. 로 끝나는 문장 검색
   - grep -r "apple.$" * : 현재 디렉토리내의 모든 파일에서 apple. 로 끝나는 문장 검색
- OR : 
   - pip list | grep -E "Tw|pl"
   - pip list | grep -e Tw -e pl
- AND :
   - cat filename | grep pattern1 | grep pattern2
   - cat filename | grep -E 'pattern1.*pattern2'

### 3) history
- 입력 했던 명령어들을 조회할 수 있다.
- history | grep ssh
- !40 : 40번째 명령어 실행

### 4) tree
- 디렉토리를 계층화하여 시각적으로 볼 수 있다.
 - tree api -L 2 -I __pycache__
    - tree <디렉토리 이름>
    - -L : 조회할 하위 디렉토리의 계층 수
    - -I : 제외할 문자

### 5) mkdir
- 디렉토리를 생성할 수 있다.
- mkdir -p ~/project/api : -p는 중간 경로 디렉토리가 없으면 자동으로 생성하라는 뜻
- mkdir {view, service, model} : 현재 위치에서 {} 안의 디렉토리를 한번에 생성

### 6) 연결된 포트 확인
- lsof -i :<포트번호>
   - list open file 의 약자 : 리눅스는 VFS(virtual file system)을 사용하므로 일반 파일, 디렉토리, 네트워크 소켓, 라이브러리 등 모든 것을 파일로 처리하고 lsof에서 상세정보를 확인 할 수 있다.
   - 5000 번 포트를 사용중인 경우 PID 확인
   - -i 옵션 뒤에 포트번호 입력 하면 해당 포트를 실행 중인 파일의 정보들이 나옴
- kill -9 <PID 번호> 
   - PID를 죽이면 해당 포트의 사용이 종료 된다. (PID는 process id의 약자)
   - kill -9는 실행중인 포트를 직접 종료하는 것이므로 여기에 실행 중인 자원이나 객체들이 제대로 정리되지 않은 채 종료 되지 않을 수 있음
   - kill -INT 또는 kill -TERM 을 사용해서 포트를 죽이는 방법 추천
- netstat 패키지를 사용하여 확인 할 수도 있다.
   - sudo apt install net-tools
   - apt를 사용하여 설치 한다.

### 7) 우분투 버전 확인
- cat /etc/issue

### 8) python 위치 확인
- which python
   - ls -lath 위치 : 자세한 내용 확인

### 9) 패지키 세부 정보 확인
- m으로 시작한 패키지 조회
- 원하는 패키지의 세부 정보 확인
```
$ pip list | grep "^m"
$ pip show 패키지이름1 패키지이름2
```

### 10) 경로 지정
- / 위치의 pwd
   - / : 시스템 디렉토리
   - / 하위에 home, bin, dev, proc, usr, sys, var, boot, etc 등의 시스템 디렉토리들이 있음
- /home의 pwd
   - /home
- 어떤 위치에서든 /, ~/을 절대경로로 사용할 수 있다. 
- ~/ 위치의 pwd
   - /home/hshkuber
- ~/project 의 pwd
   - /home/hshkuber/project

### 11) 저장공간

#### system info
- df -h : Filesystem의 size, used, avail, use%, mounted on 요약 정보
   - 저장공간 사용 현황 요약
   - df : disk free
   - -h : human-readable
- du : 디렉토리, 파일 용량 확인, 특정 디렉토리를 기준으로 하위 디렉토리와 파일의 용량 상세 확인
   - -h
   - -a : 하위디렉토리에 포함된 파일까지 전부
   - -s : 하위디렉토리 없이 전체 용량 표시
- du -ah : 하위 디렉토리별 용량 표시
- du -sh : 하위 디렉토리 없이 전체 용량 표시

#### 용량 크기 순으로 정렬하고 10개만 표시
- du -ah | sort -n -r | head -n 10
   - -ah : 하위 디렉토리 표시
   - -r : 거꾸로

#### 사용하지 않은 패키지 정리  
- sudo apt-get autoremove

### 12) shell script

#### shell 이란?
- shell : 사용자의 명령어를 해석하여 리눅스의 어떤 kernel이 실행하도록 전달하는 interpreter(해석기)
   - kernel : 운영체제의 핵심이 되는 "프로그램"
   - 사용자와 운영체지 사이를 interface 시키는 유틸리티 프로그램이다.
   - 명령어 읽고 ===> 해석하여 ===> 리눅스에 전달 ===> 실행
   - 명령을 한줄씩 해석한다.
- 여러가지 종류가 있음
   - /etc에 shells 라는 문서에 있음
   - vim /etc/shells 로 확인 가능
   - /bin/sh , /bin/bash, /usr/bin/bash, /usr/bin/sh ... 등 8가지 있음
- 윈도우는 "cmd" 가 쉘이다.   
   - powerShell : MS에서 이것을 발전시켜서 .net 2.0 기반으로 설계한 새로운 쉘
- shell programming : 쉘에 직접 명령을 날리는 것 (명령을 입력하여 실행함)
   - 명령어를 일일이 쳐서 실행하기 번거로우므로 쉘스크립트를 작성하여 실행한다.
   - 반복실행을 줄이고 스케줄링을 걸면 자동화할 수 있다.

#### shell script
- shell script : .sh 파일에 명령어를 전부 저장하고 한번에 실행되도록 만든 파일
   - 리눅스 환경에서 사용하는 파일
   - 윈도우에서는 batch file 이라고 부름
- 만드는 법
   - 제일 상단에 이 명령어를 실행시킬 쉘을 표기한다. ===> #!/bin/sh
   - 실행하려는 명령어를 연달아서 적는다. 빈칸이 있어도 됨.
   - 파일 확장자를 .sh 로 저장한다.
- 실행 방법
   - bash test_script.sh 또는 
   - sh test_script.sh 로 스크립트 파일을 실행
- **쉘 스크립트 또는 배치파일을 시스템의 환경변수에 등록하면 특정한 명령어를 단축하여 사용하거나, 시스템 실행시 자동실행 등을 할 수 있다.**

### 13) find
- 어느 위치에서든 사용하면 파일의 위치를 반환해준다.
   - sudo find / -name <파일명>
   - sudo find / -name start_* : start_로 시작하는 파일 이름을 가진 파일의 위치를 모두 반환해준다.

### 14) chmod
- chmod : change + mode
   - 파일이나 폴더의 권한permissino 설정을 한다.
- 파일 권한 요소
   - 읽기 : read ---> r
   - 쓰기 : write ---> w
   - 실행 : execute ---> x
- 디렉토리 권한 요소
   - 디렉토리의 파일 또는 디렉토리 리스트 읽기 : read ---> r
   - 디렉토리의 파일 추가, 이름 변경, 삭제 : write ---> w
   - 디렉토리에 접근 : execute ---> x
   - 디렉토리는 wx 가 함께 지정이 되어야 생성, 복사, 변경, 삭제 등의 작업이 가능함 
   - x 즉 접근권한이 없으면 w 도 할 수 없음  
- 권한의 구조 
   - 사용자 User에 대한 설정 3자리 : rwx, r-x, --x 등
   - 그룹 Group에 대한 설정 3자리 : rwx, r--, -wx 등
   - 기타 others에 대한 설정 3자리 : rwx, rw-x, r-- 등
   - 모든 사용자 All에 대한 설정 9자리 : rwx--r--r, rwxr-xrwx 등
- chmod 사용
   - chmod [option] [mode] [filename]
   - option :
      - -v : 모든 파일에 대해 진단 메시지 출력
      - -f : 에러 메시지 출력 안함
      - -c : 기존 모드가 변경되는 경우 진단 메시지 출력
      - -R : 지정한 모드를 파일, 디렉토리에 대해 재귀적으로 모두 적용 ---> 가장 많이 사용
   - mode :
      - u, g, o, a : user, group, ohters, all 설정
      - +, -, = : 현재 모드에 권한 추가 (+), 현재 모드에 권한 제거 (-), 현재 모드로 권한 지정 (=)
      - r, w, x : 읽기, 쓰기, 실행 권한
      - 기타 mode 있음
- chmod 명령의 체계
   - mode의 파라미터들을 조합하여 명령어를 만든다.
   - chmod u=rwx temp.txt : temp.txt의 사용자가 r, w, x 할 수 있는 권한을 지정한다.
   - chmod g+w temp.txt : temp.txt 파일이 속한 그룹이 w 할 수 있는 권한을 추가한다.
   - chmod o-wx temp.txt : temp.txt의 다른 사용자가 w, x 할 수 없도록 권한을 제거한다.
   - chmod go-rwx temp.txt : temp.txt를 소유한 그룹과 그외 사용자의 r, w, x 모든 권한을 제거한다.
- 8진수 형식의 파일모드 지정 방법
   - r : 4
   - w : 2
   - x : 1
   - (-) : 0
   - 이 값을 사용하여 mode 설정
   - --- : 0 ---> 아무 권한 없음
   - --x : 1 ---> 실행
   - -w- : 2 ---> 쓰기
   - -wx : 3 ---> 쓰기, 실행
   - r-- : 4 ---> 읽기
   - r-x : 5 ---> 읽기, 실행
   - rw- : 6 ---> 읽기, 쓰기      
   - rwx : 7 ---> 읽기, 쓰기, 실행
   - chmod 777 file : file의 소유 사용자, 그룹, 그외 사용자가 모든 권한을 갖는다.
   - chmod 753 file : 사용자는 7(rwx), 그룹은 5(r-x), 그외는 3(-wx)의 권한을 갖는다.
   - 8진수 방식에서는 u, g, o, a, +, -, =의 파라미터를 사용하지 못한다. 숫자에 이미 포함되어 있다.

