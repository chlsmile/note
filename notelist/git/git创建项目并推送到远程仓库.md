## git创建项目并推送到远程仓库

### create a new repository on the command line

```java```
git init
git add README.md
git commit -m "first commit"
git remote add origin https://github.com/chlsmile/manage-parent.git
git push -u origin master
```


### push an existing repository from the command line
```java```
git remote add origin https://github.com/chlsmile/manage-parent.git
git push -u origin master
```