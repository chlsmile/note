## git常用命令操作

- git config --global user.name "John Doe"
- git config --global user.email johndoe@example.com
- git config --global core.editor emacs
- git config --list
- git help config


- git init
- git add LICENSE
- git commit -m 'initial project version'
- git status -s
- git clone https://github.com/libgit2/libgit2
- git clone https://github.com/libgit2/libgit2 mylibgit

- git rm PROJECTS.md
- git rm -f PROJECTS.md
- git rm --cached README
- git mv README.md README

- git log -p -2
- git log --stat
- git log --pretty=oneline

- git commit --amend

- git reset HEAD CONTRIBUTING.md

- git branch testing

#### git log
- git log --pretty=oneline

#### git reset
- git reset --hard commit_id 回退到指定的版本
- git reset --hard HEAD^
- git reset --hard HEAD^^
- git reset --hard HEAD~100


git remote add origin git@server-name:path/repo-name.git
git push -u origin master

#### git分之合并
git merge --no-ff -m "merge with no-ff" dev

git stash
git stash list
git stash apply
git stash drop
git stash pop
git stash apply stash@{0}