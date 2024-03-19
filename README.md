### 创建项目

```
hexo init notes
cd notes
cnpm i
```

### 主题

[hexo-theme-matery](https://github.com/blinkfox/hexo-theme-matery)

[hexo-theme-matery使用文档](https://github.com/blinkfox/hexo-theme-matery/blob/master/README_CN.md)

#### 代码高亮显示问题

如果按照改了不起作用

```
hexo clean
```

```
rm -rf node_modules && cnpm install --force
```

> 修改了项目目录名称，也是执行这句

### 部署到GitHub仓库

```
echo "# notes" >> README.md
git init        # 生成.git目录
git add README.md
git commit -m "first commit"
git branch -M main
git remote add origin git@github.com:winney07/notes.git
git push -u origin main
```

1. 修改`notes\_config.yml`

   ```
   deploy:
     type: 'git' #部署的类型
     repository: https://github.com/winney07/notes.git   #仓库地址
     branch: main   #分支名称 
   ```

2. ```
   hexo clean
   ```

3. ```
   hexo g
   ```

4. ```
   hexo d
   ```

   报错：

   ```
   INFO  Validating config
   ERROR Deployer not found: git
   ```

   解决方案：

   ```
   cnpm i --save hexo-deployer-git
   ```

5. ```
   hexo d   # 再次执行
   ```

   

   如果报错：因为在项目中先执行了`git init`，解决这个报错：把目录中的`.git`目录删除

   ```
   fatal: unable to access 'https://github.com/winney07/notes.git/': Failed to connect to github.com port 443 after 21079 ms: Timed out
   FATAL Something's wrong. Maybe you can find the solution here: https://hexo.io/docs/troubleshooting.html
   Error: Spawn failed
       at ChildProcess.<anonymous> (H:\Github\notes\node_modules\_hexo-util@2.7.0@hexo-util\lib\spawn.js:51:21)
       at ChildProcess.emit (node:events:514:28)
       at cp.emit (H:\Github\notes\node_modules\_cross-spawn@7.0.3@cross-spawn\lib\enoent.js:34:29)
       at ChildProcess._handle.onexit (node:internal/child_process:291:12)
   ```

6. 在新创建的仓库中，选择`“Settings"——>”Pages"——>"**Branch**"选择"main"(选择网页所在分支)`【如果在Settings中的`Default branch`中没有显示main】

   1. `“Settings"——>”Pages"`中`GitHub Pages`中的`Branch`中选`main`-->save

   2. 在`Custom domain`中填入自定义域名`notes.winney07.cn`-->save

   3. 新建自定义域名时：

      ```
      1. 记录类型：CNAME
      2. 主机记录：vocabularies
      3. 记录值：winney07.github.io（填写cname指向的域名）
      ```

   4. 就可以访问https://notes.winney07.cn/

### 将项目源文件提交到GitHub

1. 创建`.git`目录

   如果不先执行，会报：`fatal: not a git repository (or any of the parent directories): .git`

   ```
   git init
   ```

2. 创建分支hexo并切换到hexo分支

   ```
   git checkout -b hexo 
   ```

3. ```
   git add .
   ```

4. ```
   git commit -m 'notes源文件'
   ```

5. ```
   git remote add origin git@github.com:winney07/notes.git
   ```

6. ```
   git push origin hexo
   ```

### 当前分支 `hexo` 没有与远程分支建立关联

当本地修改了内容，执行`git add .`，`git commit -m '修改备注'`，`git push` ，会报这样的错：

```
fatal: The current branch hexo has no upstream branch.
To push the current branch and set the remote as upstream, use

    git push --set-upstream origin hexo

To have this happen automatically for branches without a tracking
upstream, see 'push.autoSetupRemote' in 'git help config'.
```

> **这个错误表明当前分支 `hexo` 没有与远程分支建立关联**

方法1：

```
git push --set-upstream origin hexo
```

> 以后的推送操作中，直接使用 `git push` 而不需要指定远程仓库和分支了

方法2：也可以通过配置 `push.default` 来自动设置跟踪分支

```
git config push.default current
```
