# 1. branch 생성하기

> 2021.03.17

branch 생성 - github와 연결되어 있는 프로젝트(clone) 폴더에 들어가 다음의 명령어 입력

```
$ git branch (브랜치 이름) 
```



branch 확인 - 해당 명령어를 통해 생성된 branch 확인 가능 

``` 
$ git branch 
```

![image-20210317005601009](C:\Users\suhyeon\AppData\Roaming\Typora\typora-user-images\image-20210317005601009.png)



branch 변경하기 - checkout 명령어 사용

```
$ git checkout (브랜치 이름)
```

브랜치로 변경을 하고 원격저장소에 push를 해야함 

![image-20210317005932737](C:\Users\suhyeon\AppData\Roaming\Typora\typora-user-images\image-20210317005932737.png)

banch 반영 - upstream 명령어 사용

```
$ git push --set-upstream origin (브랜치 이름)
```



# 2. git 파일 push

```
$ git add .
$ git commit -m "OO"
$ git push
```

git add . : 변경이 일어난 모든 파일을 추적하게 함 

git commit : 수정된 내용 commit 

git push : 원격 저장소에 반영 



# 3. master 병합하기 

branch에서의 변경 사항을 'master' 브랜치에 적용(병합)하기 위한 방법

먼저 사용중인 브랜치를 'master'로 전환,

이후 하위 브랜치의 값을 merge 해준다

``` 
$ git checkout master(main)
$ git merge (브랜치 이름)
```

~~혹시 반영 안 되어 있으면 push를 해준다~~ 

