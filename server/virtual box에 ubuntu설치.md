## ⚠️ VirtualBox, Ubuntu 18.04 설치 방법 ⚠️

1. VirtualBox 설치 : [링크](https://www.virtualbox.org)
2. Ubuntu 18.04 desktop image 설치 : [[링크]](http://releases.ubuntu.com/18.04.4/?_ga=2.181027745.78635164.1595907078-93377291.1595907078) (개인적으로 홈페이지에서 받는 것은 너무 느려 [토렌트](http://releases.ubuntu.com/bionic/ubuntu-18.04.4-desktop-amd64.iso.torrent)를 활용했음)

<br>

## ⚠️ VirtualBox 상에서 Ubuntu 18.04 환경 설정 방법 ⚠️

<br>

### 가상 머신 만들기

1. VirtualBox 실행
2. '새로 만들기' 버튼 클릭
3. 이름 : 임의로 지정 / 종류 : Linux / 버전 : Ubuntu (64-bit) * 당연하지만, 64bit 운영체제가 아닌 로컬 환경이면 맞춰서 해줘야 한다.
4. 메모리 크기와 하드 디스크 크기는 원하는 만큼 지정
    - 로컬 컴퓨터 상황을 고려하여 RAM은 1GB, 하드 디스크는 20GB 지정
5. 가상 하드 디스크 파일 종류 : VMDK (Virtual Machine Disk)
    - 예전에 수강했던 운영체제 수업 때 VMDK로 하래서 했었는데, 정확한 차이는 뭘까?
6. 가상 하드 디스크 할당 형태 : 동적 할당
    - 써봐야 100MB도 쓰지 않을 것 같아서 동적 할당으로 했다.

<br>

### Ubuntu image 적용하기

1. 새롭게 만들어진 가상 머신을 클릭한 후, VirtualBox 메인에서 `설정` 버튼 클릭
2.  좌측 카테고리에서 `저장소` 클릭
3. 중앙의 `저장 장치` 섹션에서 `📋컨트롤러:IDE` 하위에 존재하는 `💿비어 있음` 클릭
4. 우측 `속성` 섹션에서 `광학 드라이브` 우측에 있는 (드랍다운보다 더 우측의) `💿 모양 버튼` 클릭
5. 다운받았던 Ubuntu desktop image 선택
6. 하단의 `확인` 버튼 클릭

<br>

### 가상 머신에 Ubuntu 설치하기 (다소 시간이 걸리고 느려도 이해하는 것이 핵심 ⭐)

1. VirtualBox 메인에서 Ubuntu image가 잘 적용되었는지 확인한 후, 상단의 `➡️시작` 버튼 클릭
2. 설치 과정 중, 맨 처음으로 `Try Ubuntu`와 `Install Ubuntu` 를 선택하는 화면이 나오는데 `Install Ubuntu` 선택
    - 해당 화면 좌측 카테고리에 언어를 선택하는 부분이 나오는데, 최대한 english로 하기를 권장.
3. `Download updates while installing Ubuntu` 체크하고 `Continue` (안 해줘도 무관하긴 하다)
4. `Erase disk and install Ubuntu` 체크하고 `Install Now` 
    - 내 로컬의 실제 disk가 아니라 가상 머신의 disk이므로 신경 쓸 필요 없다.
5. 'write the changes to disks?'라는 이름의 팝업창이 뜨며 disk partition에 대해 알려주는데, 무시하고 `Continue`
6. 마지막으로 Default로 설정할 위치를 묻는데 자동으로 Seoul이 되어있을 것이다. 아니라면 설정해주고 `Continue`
7. 관리자 계정  및 패스워드 설정 후 설치가 계속 진행 → 상당히 오래 걸리는데 문제가 없는 것이니 할 것 하고 있자.
8. 설치가 마무리되면 재시작 메세지가 뜨는데, 재시작하면 정상적으로 Ubuntu를 이용할 수 있게 된다.

*reference : [[링크]](https://ndb796.tistory.com/370)*

<br>

## ⚠️ VirtualBox 내 Ubuntu에서 SSH 환경 설정하기 ⚠️

설치하는 과정 중 업데이트를 한다고 체크했지만 혹시 몰라서 먼저 업데이트와 업그레이드를 한다.

```
$ sudo apt-get update && upgrade
```

웬만한 최신 우분투에는 OpenSSH가 탑재되어 있다고 들었는데, ssh_config를 보니 비어 있어서 설치해줬다.

```
$ sudo apt-get install openssh-server
```

아래 명령어를 이용하여 내용을 수정해주자. 이상하게 vim으로는 수정이 계속 안 됐는데 왜 그럴까?

```
$ sudo nano /etc/ssh/ssh_config
```

ssh_config에서 아래와 같이 내용을 수정해준 후 저장했다. 

- 기본적으로 SSH는 포트 22에서 수신을 대기하기 때문에 `Port 22의 주석을 해제`
- 포트번호 아래에 `MaxAuthTries 4`를 넣어줘서 최대 로그인 횟수를 4회로 제한
- 그리고 비밀번호로 authenfication을 확인할 수 있도록 `PasswordAuthentification no의 주석을 해제`하고 `no`를 `yes`로 변경

이후, 로컬 환경에서 접속할 때 문제가 없도록 아래 명령어를 이용해 방화벽을 해제해줬다.

```
$ sudo ufw enable
$ sudo ufw allow 22
$ sudo ufw reload
```

그리고 Ubuntu를 종료한 뒤, 로컬에서 가상 OS에 접근할 수 있도록 호스트 네트워크를 설정해줘야 한다. 아래 순서대로 진행했다.

1. VirtualBox 메인에서 가상 머신을 클릭한 후 `설정` 클릭
2. 좌측 카테고리의 `네트워크` 클릭
3. `어댑터 2` 클릭
4. '다음에 연결됨' 우측의 드랍다운에서 `호스트 전용 어댑터` 클릭
5. '이름' 우측의 드랍다운에서 `VirtualBox Host-Only Ethernet Adapter` 클릭
6. `확인` 클릭
- 만약 5번에서 `VirtualBox Host-Only Ethernet Adapter`가 보이지 않는다면 직접 만들어줘야 한다. [[참고 링크]](https://cjwoov.tistory.com/3)

Ubuntu를 재시작하고 ssh를 다시 시작해준다. 

```
$ sudo service ssh start    # SSH 서비스 실행
$ sudo service ssh stop     # SSH 서비스 중단
$ sudo service ssh restart  # SSH 서비스 재시작
```

최종적으로 제대로 구동되는지 확인하기 위해 아래 명령어를 이용해 net-tools를 설치했다.

```
$ sudo apt install net-tools    # net-tools 설치
```

그 후, 아래 명령어들을 이용해 구동되는지 확인했다. 정상적으로 running되고 있는 것을 확인했기에 다음 단계로 넘어간다.

```
$ echo -e "\n" && sudo ps -ef | grep sshd && echo -e "\n" && sudo netstat -ntlp | grep sshd
$ sudo service ssh status
```

<br>

## ⚠️ root 계정 이외에 본인 접속할 계정 추가하기 ⚠️

아래의 명령어를 사용해 새로운 계정을 만들고 비밀번호를 설정했다.

```
$ sudo useradd temp		# temp라는 계정을 생성
$ sudo passwd temp		# 계정 temp의 비밀번호 설정
```

계정 temp는 현재 홈 디렉토리와 그룹, 쉘이 설정되지 않아 지정해줘야 한다.

1. 홈 디렉토리 생성 및 권한 부여

    ```
    $ sudo mkdir -p temp
    $ sudo chown -R temp:temp /home/temp/
    ```

   2. 계정 temp에 그룹을 할당해주고 확인

```
$ sudo usermod -G temp temp
$ id temp
```

   3. 기본 쉘이 설정되어 있나 확인. 나는 기본적으로 설정되어 있었다.

```
$ cat /etc/passwd | grep temp
```

<br>

## ⚠️ 로컬 컴퓨터에서 가상 환경 리모트 컴퓨터에 ssh로 접속해서 본인 계정으로 로그인하기 ⚠️

로컬 컴퓨터에서 가상 환경 리모트 컴퓨터에 접속하는 방법은 다양한데, 그 중 putty를 활용하는 방법을 선택했다. 어떠한 방식을 이용하든,  원격 접속의 대상이 되는 가상 OS의 IP를 확인해야 한다. 이전에 호스트 네트워크를 설정해주었으니 아래 명령어를 통해 호스트 네트워크의 IP를 확인했다.

- 첨언하자면, 1번 mission을 마친 후 기존에 이용하고 있던 WSL2에서 OpenSSH를 설치하니 WSL2와 VirtualBox 상의 Ubuntu 간의 리모트가 가능해졌다. 방법을 몰라서 putty를 썼던 건데, 앞으로는 그냥 WSL2를 사용하자.

```
ifconfig
```

putty를 설치하고 실행한 후, 초기 화면에서 아래와 같이 기입한다.

- Host Name : 호스트 네트워크의 IP주소
- Port : 22
- Saved Sessions : Ubuntu

Save버튼을 눌러 저장한 후, Open한다. 그 다음,새롭게 만든 계정의 아이디와 패스워드를 입력하여 가상 환경 리모트 컴퓨터에 접속한다.