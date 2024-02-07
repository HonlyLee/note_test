# Git的基本使用
## 创建一个本地的Git项目仓库
1. clone别人的项目仓库

命令：==**git clone**== 项目地址

![clone](\git_photos/clone_.gif)

2. 自己创建文件夹

> 在**创建的文件夹内**右键选择出控制台输入命令后自动创建

命令：==**git init**==

***
## 提交的三个步骤

1. **修改文件内容**
> 即本次修改后的版本

2. **git add**

> 添加相应的文件到暂存区（可理解为打包）

*命令*：==**git add 文件名**==
> 若是添加文件夹内所有文件则使用`git add .`
3. **git commit**
> 进行提交

命令：
- ==**git commit**==
- ==**git commit -m "备注内容"**==
> 后者多了备注


## 查看历代版本信息

- 基本信息

命令：==**git log**==
    ![](/Git_using/git_photos/git_log.png)
> 包含作者、备注、时间


- 其他信息

命令：==**git log --stat**==

> 可查看每个版本修改了哪些文件

- 查看某次版本具体修改部分

命令：==**git diff**== **(后面跟某个版本的commit ID,可通过上条命令查看)**

## 对版本的回溯、分支操作
1. **代码回溯**
命令：
- ==**git reset --hard[commit id]**==
- ==**git checkout [commit id]**==

> 两者有一定区别，可转到[该处]()查看。

2. **分支**
   1. <u>*查看分支*</u>
   命令：==**git branch**==
   > 默认一开始为**master**分支,该分支一般为稳定不变的代码
   2. <u>*创建分支*</u>
   命令：==**git checkout -b [branch name]**==
   > 该分支一般为进行开发进行中的代码工作。一般**创建完分支后**，==停留在当前分支==
   3. **切换分支**
   命令：==**git checkout [branch name]**==
   4. **合并分支**
   命令：==**git merge [branch name]**==
   > 通常**停留在==master==分支**，将**其他分支合并进来**

   ## vscode&Git
jhbhjbjhj






