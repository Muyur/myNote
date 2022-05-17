### 如何关联VScode和Github/Gitee

#### 创建一个新的空仓库

Github

![image-20211125171837781](C:\Users\admin\AppData\Roaming\Typora\typora-user-images\image-20211125171837781.png)

Gitee

![image-20211125171930370](C:\Users\admin\AppData\Roaming\Typora\typora-user-images\image-20211125171930370.png)

#### 进行Git全局配置

```
git config --global user.name "xxx"
git config --global user.email "xxx@xx.com"
```

#### 创建Git仓库

如果还没有仓库 :

```
mkdir myProject
cd myProject
git init
git commit -m "first commit"
git remote add origin https://xxx.com/xxx/xxx
git push -u origin master
```

如果已经有仓库 :

```
cd myProject
git remote add origin https://xxx.com/xxx/xxx
git branch -m master main  // 更改默认分支名称
git push -u origin main
```

### 更新部署在Github中的项目

1. 在被部署的项目文件中打开`Git Bush Here`
2. 执行`git add .`指令提交到暂存区
3. 执行`git commit -m "xxx"`指令,提交到本地仓库
~~4. 执行`git push -u origin master`指令提交到远程仓库
4. 执行`git push -u origin main`指令提交到远程仓库
