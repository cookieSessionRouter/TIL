# branch 전략 (Git-Flow, Git-Workflow, Gitlab-Workflow)

### (1) Git-Flow

브랜치를 크게 `메인 브랜치(Main branch)`, `피처 브랜치(Feature branch) 혹은 토픽 브랜치(Topic branch)`, `릴리스 브랜치(Release branch)`, `핫픽스 브랜치(Hotfix branch)`와 같이 4가지로 나누어 개발하는 전략을 일컫는다. 

<br>

가장 중심이 되는 주 브랜치는 `master`와 `develop` 브랜치이며, merge된 `feature`, `release`, `hotfix` 브랜치는 삭제하는 방향으로 구성되어 있다. 큰 흐름은 다음과 같다.

1) master 브랜치에서 develop 브랜치를 분기시킨다.
2) 개발자들은 develop 브랜치에 자유롭게 커밋을 한다.
3) 기능 구현이 있는 경우, develop 브랜치에서 feature 브랜치를 분기한다.
4) 배포를 준비해야 하는 경우, develop 브랜치에서 release 브랜치를 분기한다.
      - 테스트를 진행하면서 발생하는 버그 수정은 release 브랜치에 직접 반영한다.
      - 혹자는 hotfix 브랜치에서 버그 수정을 한다고 한다. 아무튼 서브 브랜치인 것은 틀림없다.
5) 테스트가 완료되면 release 브랜치를 master와 develop 브랜치에 merge한다.

위 흐름이 절대적인 것은 아니며, 필요에 따라 다양한 브랜치가 분기될 수 있고 더 적은 브랜치만을 사용할 수도 있다.

<br>

Git-Flow 전략은 주기적으로 배포를 해야하는 프로젝트에는 적합하다는 장점이 있다. 즉, 전통적인 waterfall 방식 등에서 유리한 브랜치 전략이라고 할 수 있다. 하지만 브랜치가 많아 복잡하고 어떤 프로젝트에 따라서는 몇몇 브랜치가 애매한 포지션을 가질 수 있다는 단점이 있다. 특히 지속적인 통합 및 배포가 가능해진 요즘에는 배포 가능한 버전을 만들기 위해 사전 작업이 많이 필요하기 때문에, 기민하게 대처하기 힘들어 문제가 발생할 수 있다.

<br>

### (2) Git-Workflow

`Git-Flow`의 흐름을 이어가되, 언제나 배포 가능한 빌드를 만들기 위한 방안으로 등장한 브랜치 전략이다. Git-Flow가 배포를 위한 `release` 브랜치를 따로 두고 집중적으로 테스트를 하는 것과 달리, Git-Workflow는 `commit`이나 `feautre` 브랜치에서 테스트를 완료하고 PR(Pull Request)와 Code Review를 거쳐 곧바로 `master` 브랜치에 merge하는 방식이다.

`release` 브랜치를 생략하기 떄문에 항상 배포 가능한 상태를 유지할 수 있게 된다는 장점이 있다. 하지만 자율적인 테스트에 의존하기 때문에 빌드의 안정성이 떨어질 우려가 있다는 단점도 존재한다.

<br>

### (3) Gitlab-Workflow

Github에서 말하는 `Git-Flow` 전략에서 발생할 수 있는 문제들을 보완하기 위해 등장했다. 대부분의 흐름은 Git-Flow 전략과 유사하지만, `develop`와 `staging`, `production` 브랜치를 항시 유지시킨다는 차이점이 있다. 각 브랜치는 아래와 같은 역할을 수행한다.

`develop` : 개발자들이 PR을 통해 커밋을 최초로 등록하는 브랜치다. 테스트가 덜 된 commit들이 존재할 수 있고, production 배포와 관계가 없으므로 큰 부담없이 개발자들이 commit하는 브랜치이다.

`staging` : develop 브랜치의 환경에서 테스트를 마치고 배포가 결정된 commit들을 옮겨놓는 브랜치이다. production과 동일한 환경에서 테스트되기 때문에 배포되는 기능 혹은 버그 수정에 집중할 수 있다. 즉, 맨 처음의 Git-Flow에서 release 혹은 hotfix 브랜치의 기능을 여기서 담당하는 것이다.

`production` : staging 브랜치에서 테스트를 마친 후, production 브랜치를 staging 브랜치로 merge한다. 그렇게 되면 안정적으로 staging 브랜치에서 테스트를 마친 상태라 바로 안정적인 배포가 가능하게 된다.

<br>

### 총평

아무래도 시간의 흐름에 따라 기존의 브랜치 전략의 단점을 보완하기 위해 발전된 형태이기 때문에 `gitlab workflow`가 효율적이라고 생각된다. 특히 agile이 강조되는 요즘 분위기 속에서 `git-flow`는 비효율적이라고 생각되고, 많이 선호되지도 않을 것 같다.

학부에서 진행하는 아기자기한 프로젝트도 커뮤니케이션이 원활하지 않아 git conflict가 일어나는 경우가 아주 많았다. 이러한 브랜치 전략에 대해 처음으로 공부해봤는데, 이렇게 체계적으로 룰을 정하고 세세하게 관리함으로써 불필요한 커뮤니케이션은 줄이고 업무의 효율을 극대화할 수 있을 것이라고 생각한다.

<br>

_reference_

1. [Git 브랜칭 전략 : Git-flow와 Github-flow](https://hellowoori.tistory.com/56)
2. [지속적 통합/배포(CI/CD)를 위한 Git Workflow 전략](https://blog.ull.im/engineering/2019/06/25/git-workflow-for-ci-cd.html)
