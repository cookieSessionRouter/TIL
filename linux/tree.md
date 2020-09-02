# tree

1. 설치

   ```shell
   sudo apt-get install tree
   ```

<br>

2. 사용법

   특정 디렉토리에서 아래 명령어를 치면 현재 디렉토리부터 하위 디렉토리의 구조를 출력해준다.

   ```shell
   tree
   ```

    ![](/images/일반적인tree.PNG)

<br>

3. 옵션

   [map page](https://linux.die.net/man/1/tree) 참고

<br>

4. 자주 썼던 옵션

   (1) 특정 디렉토리 혹은 파일을 제외하고 tree를 출력해주고 싶을 때

   ```shell
   tree -I "[regular expression pattern]"
   ```

   예시

   - javascript express 프로젝트에서 node_modules를 제외하고 tree 출력

     ```
     tree -I "node_modules"
     ```

     ![](/images/node_module_제외.PNG)

   <br>

   - README.md에 이미 .gitignore에 포함되어 있는 의미없는 파일을 제외하고 구조를 넣어주고 싶을 때, 정규표현식을 통해 의미없는 것들을 다 제외시켜줄 수 있음.

     ```
     tree -I "*.sh|node_modules|*.jpg|*test*"
     ```

     ![](/images/제외_커스터마이징.PNG)
