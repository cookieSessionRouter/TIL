1. [Git 설치](https://git-scm.com/download/linux)

```bash
$ sudo apt-get install git
```

<br>

2. curl 설치

```bash
$ sudo apt-get install curl
```

<br>

3. curl 기반 heroku CLI 설치

```bash
$ curl <https://cli-assets.heroku.com/install.sh> | sh
```

![](./images/curl설치.PNG)

<br>

4. npm 명령어로 heroku 설치

```bash
$ sudo npm install -g heroku
```

![](./images/heroku_npm.PNG)

<br>

5. heroku가 정상적으로 설치되었는지 확인

```bash
$ heroku --version
```

![](./images/heroku_version.PNG)

<br>

6. 헤로쿠 계정 생성

https://www.heroku.com/ 가서 계정 생성

<br>

7. app 생성

https://victorydntmd.tistory.com/112 참고

<br>

8. 터미널에서 아래 명령어 수행 후, 아무 키나 누르기. → 이후, 사이트가 뜨면 `로그인` 버튼 클릭.

```bash
$ heroku login
heroku: Press any key to open up the browser to login or q to exit
 ›   Warning: If browser does not open, visit
 ›   <https://cli-auth.heroku.com/auth/browser/***>
heroku: Waiting for login...
Logging in... done
Logged in as yhw8258@naver.com
```

![](./images/heroku_login.PNG)

<br>

9. 배포하고자 하는 디렉토리로 이동 후, 아래 명령어 수행. 로컬에 있는 디렉토리를 heroku 내 원격저장소에 연결하는 과정이다.

```bash
$ heroku git:remote -a [app name]
```

- 나는 heroku 사이트에서 app 이름을 `boostcamp-j131-project1-airbnb`로 만들었기 때문에 아래와 같이 명령어를 썼다. 그러면 아래 `set git remote heroku to ~`이라는 문구가 뜬다.

  ```bash
  $ heroku git:remote -a boostcamp-j131-project1-airbnb
  set git remote heroku to <https://git.heroku.com/boostcamp-j131-project1-airbnb.git>
  ```

- `git remote -v` 명령어를 통해 연결된 원격저장소를 확인해보면 `heroku`가 추가된 것을 알 수 있다.

  ![](./images/git_remote_after_heroku_installation.PNG)

<br>

10. 연결된 로컬 디렉토리 내 파일들을 heroku 원격 저장소로 push하자. 이때 [브랜치] 안에는 푸시하고자 하는 브랜치를 넣으면 된다.

```bash
$ git push heroku [브랜치]
```

- 현재 push할 수 있는 브랜치는 무엇이 있나 확인해보자.

  ```bash
  $ git branch -a
  ```

  ![](./images/git_branch-a.PNG)

- feature 브랜치는 특정 기능을 만든 후 사라지는 임시적인 브랜치이므로 master 브랜치를 배포하자. 과제를 하면서 upstream을 포크해왔기 때문에, 현재의 구조로는 master 브랜치가 J131이라고 할 수 있다. 단, 이때 브랜치 이름이 master나 main이 아니면 heroku에서 build를 해주지 않으므로, J131 브랜치가 [master임을 명시해주는 옵션(~`:master`)을 달아줘야 한다](https://stackoverflow.com/questions/14593538/make-heroku-run-non-master-git-branch).

  ```bash
  $ git push heroku J131:master
  ```

  ```bash
  오브젝트 나열하는 중: 2276, 완료.
  오브젝트 개수 세는 중: 100% (2276/2276), 완료.
  Delta compression using up to 8 threads
  오브젝트 압축하는 중: 100% (1644/1644), 완료.
  오브젝트 쓰는 중: 100% (2276/2276), 2.15 MiB | 1.64 MiB/s, 완료.
  Total 2276 (delta 507), reused 2205 (delta 483)
  remote: Compressing source files... done.
  remote: Building source:
  remote:
  remote: -----> Node.js app detected
  remote:
  remote: -----> Creating runtime environment
  remote:
  remote:        NPM_CONFIG_LOGLEVEL=error
  remote:        NODE_ENV=production
  remote:        NODE_MODULES_CACHE=true
  remote:        NODE_VERBOSE=false
  remote:
  remote: -----> Installing binaries
  remote:        engines.node (package.json):  unspecified
  remote:        engines.npm (package.json):   unspecified (use default)
  remote:
  remote:        Resolving node version 12.x...
  remote:        Downloading and installing node 12.18.3...
  remote:        Using default npm version: 6.14.6
  remote:
  remote: -----> Installing dependencies
  remote:        Installing node modules (package.json + package-lock)
  remote:
  remote:        > nodemon@2.0.4 postinstall /tmp/build_e8b8dcb7/node_modules/nodemon
  remote:        > node bin/postinstall || exit 0
  remote:
  remote:        Love nodemon? You can now support the project via the open collective:
  remote:         > <https://opencollective.com/nodemon/donate>
  remote:
  remote:        added 216 packages from 104 contributors and audited 218 packages in 6.016s
  remote:
  remote:        13 packages are looking for funding
  remote:          run `npm fund` for details
  remote:
  remote:        found 0 vulnerabilities
  remote:
  remote:
  remote: -----> Build
  remote:
  remote: -----> Caching build
  remote:        - node_modules
  remote:
  remote: -----> Pruning devDependencies
  remote:        audited 218 packages in 1.89s
  remote:
  remote:        13 packages are looking for funding
  remote:          run `npm fund` for details
  remote:
  remote:        found 0 vulnerabilities
  remote:
  remote:
  remote: -----> Build succeeded!
  remote: -----> Discovering process types
  remote:        Procfile declares types     -> (none)
  remote:        Default types for buildpack -> web
  remote:
  remote: -----> Compressing...
  remote:        Done: 25.3M
  remote: -----> Launching...
  remote:        Released v3
  remote:        <https://boostcamp-j131-project1-airbnb.herokuapp.com/> deployed to Heroku
  remote:
  remote: Verifying deploy... done.
  To <https://git.heroku.com/boostcamp-j131-project1-airbnb.git>
   * [new branch]      J131 -> master
  ```

<br>

11. 참고했던 블로그에서는 push 후 아래 명령어를 수행하라고 한다. [다른 블로그](https://bcho.tistory.com/1090)에서 찾아보니 스케일링을 하는 명령어다. 근데 공식 문서는 아니고 어떤 [다른 문서](https://tour.dlang.org/tour/en/vibed/deploy-on-heroku)를 보니 여기서 수행하는 명령어는, 스케일링을 한다기보다 자고 있는(sleep) 상태의 dyno를 깨워주는 명령어인 것 같다. 깨워주지 않으면 request를 받지 못한다고 하네?

```bash
heroku ps:scale web=1
```

<br>

12. 배포는 완료됐다. 배포한 프로젝트를 확인하기 위해 링크로 들어가서 확인해보자. 링크를 확인하는 방법은 다음과 같다.

- https://[heroku dashboard에 보이는 app이름].herokuapp.com/

  ex) https://boostcamp-j131-project1-airbnb.herokuapp.com/

- heroku dashboard에서 app을 클릭 → 우측 상단에 위치하는 `open app` 버튼 클릭

- 터미널에서 아래 명령어를 수행하면 app의 home이 자동으로 열린다고 한다. 하지만 WSL2에서는 어떤 이슈인지는 모르겠지만 `error opening web browser.`를 자꾸 내뱉어서 수동으로 들어가라고 url을 보여준다.

  ```bash
  $ heroku open
  ```

<br>

13. 나중에 배포 과정 중 에러가 생기면 아래 명령어를 통해 확인하자.

```bash
$ heroku logs

# -n 옵션을 주면 설정한 숫자만큼 최근에 발생한 log를 확인할 수 있음
# ex) $ heroku logs -n 10

# --tail 옵션을 주면 log 출력 후, 계속 log를 볼 수 있도록 log창이 꺼지지 않음
# ex) $ heroku logs --tail
```

<br>

_reference_

[Node.js\] Heroku로 배포( deploy )하기](https://victorydntmd.tistory.com/112)

[Heroku CLI Commands](https://devcenter.heroku.com/articles/heroku-cli-commands)

[The Heroku CLI - Download and install](https://devcenter.heroku.com/articles/heroku-cli#download-and-install)

[Heroku에서 스케일링 하기](https://bcho.tistory.com/1090)

[Deploy on Heroku](https://tour.dlang.org/tour/en/vibed/deploy-on-heroku)
