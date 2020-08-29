# git add, git commit 시 내부 동작 흐름

본격적인 서술에 앞서 용어를 간략히 정리하자.

* 개인이 작업하는 공간 : `Working Directory`
* Git 로컬 데이터베이스 : `Git Directory`

`git init` 혹은 `git clone`을 하여 git이 활성화된 이후, `Working Directory`에서 수정하거나 새롭게 작성한 파일들이 아직 `Git Directory`에 commit되지 않았다면 해당 파일 및 디렉토리들을 `modified` 상태라고 한다.

`modified` 상태의 파일 및 디렉토리를 `git add`하게 되면 해당 파일 및 디렉토리들은 `Stage`된다. git은 파일들을 델타 기반의 버전 관리가 아닌 스냅샷의 스트림처럼 취급하기 때문에, stage된다는 것은 commit할 스냅샷을 만든다고 이해하면 좋다. git add를 할 때에는 명령어 옵션을 사용하여 수정된 파일만 추가할 수도, 일부 파일만 추가할 수도, 모든 파일을 추가할 수도 있다.

> 델타 기반의 버전 관리 시스템은 각 파일의 변화를 시간순으로 관리하면서 파일들의 집합을 관리하는 방식으로, 스냅샷의 스트림처럼 취급하는 방식보다 크기가 방대하고 속도도 느리다. 또한, 스냅샷의 스트림처럼 취급하게 되면 파일의 변화가 없는 경우 성능 향상을 위해 파일을 새로 저장하지 않고 이전 상태의 파일에 대한 링크만 저장하게 된다.

`Stage`되어 `Staging Area`로 이동하게 된 파일 및 디렉토리들은 `staged `상태라고 부느는데, 현재 수정한 파일을 곧 `commit`할 것이라고 표시한 상태를 의미한다. `Staging Area`에 있는 파일들을 `commit`하면 `Git Directory`에 영구적인 스냅샷으로 저장된다.

![워킹 트리](https://lh6.googleusercontent.com/AK5BcQC6DCXHIdUFCH4Nmo8EQ46zoR4gUl_AIuqRq-37lK14OVFU9TYDciSOLDZiskUKdGwdTjuwIHmU5HQmmx78KZr11r3M8EUeeVLrM_tbSLRfDwwvR0Ioy4Owy-cLXwhunJHV)



_reference_
1. [1.3 시작하기 - Git 기초](https://git-scm.com/book/ko/v2/%EC%8B%9C%EC%9E%91%ED%95%98%EA%B8%B0-Git-%EA%B8%B0%EC%B4%88)
