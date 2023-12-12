# git cherry-pick

```bash
git cherry-pick [커밋 해시]
```

    

# cherry-pick 중 충돌 났을 때

main 브랜치에서 local 브랜치의 커밋을 끌어올려고 할 때, 충돌 났을 경우

```java
git reset --hard [commit hash]  // main에서 main의 이전 커밋id
git cherry-pick  [commit hash]  // main에서 local커밋 중 가져올 커밋id
```

- 세부 설명
    
    아래 명령어로 main을 충돌나지 않는 이전 커밋으로 깔끔하게 되돌린다. --hard 명령어이기 때문에 working tree에 작업 내용들도 다 날라가기 때문에 커밋이 깔끔해지고 이후에 cherry-pick으로 끌어오면 된다
    
    ```java
    git reset --hard [commit hash]
    ```
    

상황

로컬에서 작업한 것 중 하나를 메인에서 체리픽 해올려는 상황

메인에서 로컬꺼를 체리픽하니 충돌발생

충돌에서 헤드쪽만 제거하면 될 줄 알았는데 파일 상태가 메인 쪽 상태하고 로컬의 뒷부분하고 섞여 있는 이상한 상태임

해결책 : git checkout 브랜치명 -- 경로/파일

```java
// 특정 브랜치에서 특정 파일을 가져오는 방법
git checkout 브랜치명 -- 경로/파일

```

# git cherry-pick -e

체리픽 해 온 커밋을 그대로 가져오는 게 아닌 커밋 메세지 수정

```java
git cherry-pick -e [커밋 해시]
git cherry-pick --edit [커밋 해시]
```

# git cherry-pick -n, --no-commit

체리픽하면서 자동 커밋 금지

```jsx
git cherry-pick -n [커밋 해시]
git cherry-pick --no-commit [커밋 해시]
```

