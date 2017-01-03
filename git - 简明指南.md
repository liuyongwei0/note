* 创建新仓库
	* 创建仓库文件夹, 并进入文件夹
	* git init : 创建新的git仓库(会生成.git文件夹)
* 克隆远程仓库
	* git clone 远程仓库的地址(https://github.com/zxfjd3g/H50510_pre.git)
* 工作流
	* 你的本地仓库由 git 维护的三棵“树”组成
	* 第1个: 工作区(working dir) 你的工作目录
	* 第2个: 暂存区（Index/Stage）它像个缓存区域，临时保存你的改动
	* 第3个: 版本区(HEAD), 它指向你最后一次提交的结果
* 添加和提交
	* 将工作区的新增/修改提交到暂存区: git add <filename>/*
	* 将暂存区的更新提交到版本区(HEAD) : git commit -m "代码提交信息"
		* 查看状态: git status
		* vim操作
			插入模式（按i键进入）
			正常模式（按esc进入）
			ZZ 保存并退出
* 推送改动
	* 如果不是克隆的仓库, 第一次需要先关联上远程仓库: git remote add origin url(远程仓库的地址)
	* 将本地版本区(HEAD)的更新推送到远程仓库 : git push origin master
	* 提示输入username
	* 提示输入password
* 分支
	* 查看所有分支: git branch
	* 创建一个叫做“feature_x”的分支，并切换过去 : git checkout -b feature_x
	* 创建新文件(x.txt),并添加提交: git add * --->git commit -m "new x file"
	* 切换回主分支 : git checkout master
	* 推送到远程仓库: git push origin feature_x
	* 删掉新建的分支 : git branch -D feature_x
	* 
* 更新与合并
	* 将远程最新版本拉到本地: git pull origin master
	* 比较2个分支版本的区别: git diff <source_branch> <target_branch>
	* 合并分支: git merge <branch>
	* 在更新或合并时可能会出现冲突, 解决冲突
		* 打开文件修改文件内容
		* git add *
		* git commit -m "resolve conflict"
* 标签(备份重要版本)
	* 查看提交日志 : git log (按Q退出)
	* 给重要版本创建标签: git tag 1.0.0 1b2e1d63ff(某个提交ID)
	* 将工作区切换到标签版本: git checkout 1.0.0
* 替换本地改动
	* 使用HEAD中的最新内容替换掉你的工作目录中的文件 : git checkout -- <filename>
	* 丢弃你在本地的所有改动与提交 : git fetch origin --> git reset --hard origin/master

--------------------------------------------------------------------
查找关注大的项目: stars:>1000