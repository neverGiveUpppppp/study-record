# 마지막 커밋 내역 제외한 이전 커밋 삭제하기

```java
git reset --hard HEAD~n
```

**`n` :** 지우고자 하는 이전 커밋의 수  


  
  
ex)

```java
git reset --hard HEAD~2 // 현재커밋 제외한 이전 2개의 커밋 삭제

// 커밋id가 1-10이 있다고 가정하고 가장 최근 커밋이 10
// 10을 제외한 6-9까지의 커밋 내역을 삭제할려면
git reset --hard HEAD~4   // 1-5와 10의 커밋내역이 남음
```

```java
git reset --hard HEAD~n
git push origin [브랜치명] --force // reset 이후 강제 푸쉬 해야함
```

- **`-force`** : 강제로 푸쉬하는 옵션
