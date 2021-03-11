## Git

### 1.git分支从master切换到main

现在 git 已经支持 main 分支了。本地分支是 master，但远程仓库为main，而提交的时候总是会给远程仓库自动创建一个 master 分支，不喜欢。so，let's go ~

```bash
git checkout -b main
# Switched to a new branch 'main'

git branch
# * main
#  master

git merge master # 将master分支合并到main上
# Already up to date.

git pull origin main --allow-unrelated-histories # git pull origin main会报错：refusing to merge unrelated histories
git push origin main
```

### 2.删除分支

```bash
# 删除本地master分支
git branch -d master
# 删除远程分支
git push origin :master
```

### 3.删除远程仓库文件或目录

```bash
# 删除a目录下的2.txt文件
git rm -r --cached a/2.txt

# 删除a目录
git rm -r --cached a

# 提交
git commit -m "xxxxx"
git push
```

删除本地仓库中的文件 `git rm --cached a.txt` （删除本地文件夹方法一样）

### 4.OpenSSL SSL_read: Connection was reset, errno 10054

这是服务器的SSL证书没有经过第三方机构的签署，所以报错。

解决办法：`git config --global http.sslVerify "false"`