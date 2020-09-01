# npm (Node Package Manager)

`npm init`

새로운 프로젝트나 패키지를 만들 때 사용하는 명령어. 프로젝트를 시작할 때 가장 먼저 쓰는 명령어다.

> package.json
>
> 프로젝트의 정보를 정의하고, 의존하는 **패키지 버전 정보**를 명시하는 파일.

<br>

`npm install` (= `npm i`)

패키지를 설치하는 명령어.

- `npm install [package]@[version]` : 특정한 버전의 패키지 설치
- `npm install [address]` : 특정한 저장소에 있는 패키지를 설치. 주로 특정 깃허브에 있는 패키지를 설치할 때 이용.

* `-s` 혹은 `--save` 옵션 : 패키지를 설치하며 dependencies에 패키지를 추가. npm5부터는 --save옵션이 기본적으로 설정되어 있기 때문에 안 붙여도 된다고 함.
* `--save-dev` 또는 `-D` 옵션 : 패키지를 설치하며 devDependencies에 패치지를 추가.
* `-g` 옵션 : 패키지를 설치하며 글로벌에 패키지를 추가. 주로 계속 쓰이는 명령어를 설치할 때 사용.

> dependencies : **프로덕션 환경**에서 응용 프로그램에 필요한 패키지.
>
> devDependencies : **로컬 개발 및 테스트**에만 필요한 패키지.

<br>

`npm update`

설치한 패키지를 업데이트하는 명령어.

<br>

`npm dedupe`

npm의 중복된 패키지들을 정리하는 명령어. 가끔 쳐주면 용량을 줄일 수 있음.

<br>

_reference_

[npm 명령어](https://www.zerocho.com/category/NodeJS/post/58285e4840a6d700184ebd87)

[package.json 알아보기](https://velog.io/@skyepodium/package.json)

[개발용 라이브러리와 배포용 라이브러리 구분하기](https://joshua1988.github.io/webpack-guide/build/npm-module-install.html#개발용-라이브러리와-배포용-라이브러리-구분하기)
