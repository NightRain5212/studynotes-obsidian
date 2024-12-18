

# githubdesktop的使用

- 本地仓库分区
	- 存储区（存储仓库文件）
	- 工作区（修改工作区的文件，但并不是修改仓库中的文件）
	- 暂存区（在两者之间进行比对操作）

- 创建本地仓库
- 删除本地仓库
	- 删除软件中的仓库（不删除本地仓库）
	- 删除本地仓库（移动至回收站）
- 识别文件
	- 可以自动识别仓库路径下的文件（要与.git路径区分开）
	- 操作文件是在仓库路径，存储文件在仓库是在.git路径
- 比对文件
	- 比对仓库路径下的操作文件，与仓库中存储的存储文件（.git中）
- 提交文件（commit）
	- 将仓库路径的文件提交到仓库中。
	- 当提交的文件与存储文件不同时，等同于创建了一个版本号不同的新文件
- 版本号：40个16进制的数字（提交码）（SHA-I加密）
	- 使用版本号查看文件（命令）
		- 定位仓库中的文件（版本号2+38：前两位对应文件夹，后38对应文件名）
		- 查看文件，在仓库路径下打开git bush，使用`git cat-file -p 版本号`
			- tree后面的一大串也是一个版本号，用此版本号查看文件的提交信息
			- parent 后面的是上一次提交的版本号
			- 查看tree后面的版本号，得到文件的（状态信息）数字+空格+单词+空格+数字（版本号）
			- 再次查看即可看到文件内容
	- 依次查看的是：文件的提交信息->文件的状态信息->文件内容
	- 提交文件时，新增提交信息，新增状态信息（关联到新文件和旧文件），新增文件内容
	- 修改文件时，新增提交信息，新增状态信息（关联到旧文件和新文件），新增文件内容（修改后的文件）
	- 删除文件时，新增提交信息，新增状态信息（只关联旧文件）
	- HEAD文件
		- 存放一个路径（为当前所处分支的对应路径）
		- （路径指向的文件内容为对应分支最新提交的文件的版本号）
- 暂存区
	- 位于存储区与工作区之间（进行比对操作）
	- 工作区-(add)->暂存区-(commit)->存储区
- 删除文件
	- 删除本地文件时，仓库文件还没被删除。
	- 若要删除仓库文件，仍需commit。
- 分支
	- 多人协同开发时，每个人针对同一个资源仓库的不同副本仓库进行操作，最后再进行分支合并。
	- 创建分支
	- 提交文件：
		- 是提交到当前选中的分支中，不同的分支实际上是不同的仓库（之间不能互相访问）
	- 分支合并(merge)
		- 合并时若有相同文件，则会造成文件冲突，只要按提示打开冲突文件，删除不需要的内容即可。
- 标签
	- 可以在历史记录中右键添加tag，里面输入你想描述的内容
- 远程仓库
	- 储存在中央服务器的仓库
	- clone：将远程仓库下载到本地
	- push：将本地仓库上传到远程仓库
	- gitee远程仓库（国内的远程仓库管理）
- README
	- 添加项目的重要描述信息
- 忽略文件ignore
	- 服务器不会把忽略的文件上传到仓库中

# git命令

- 通过命令在不同区转移文件
	- 工作区-(add)->暂存区-(commit)->存储区
	- 远程仓库--(clone)->存储区
	- 工作区--(publish)->远程仓库
	- 暂存区--(push)->远程仓库
	- 远程仓库--(pull)->暂存区

- 在当前路径创建仓库
	- `git init` 初始化仓库
- 从远程仓库克隆
	- `git clone 地址 仓库名`
- 配置
	- `git config user.name 用户名`
	- `git config user.email 邮箱`
	- `git config --global user.name 用户名` 全局配置
- 查看状态
	- `git status`
-  add
	- `git add 文件名` ，添加至暂存区（包括删除文件的操作）
	- `git rm --cached 文件名` ，从暂存区删除
- commit
	- `git commit -m 消息`，为操作添加信息说明
- log日志
	- `git log` ，查看提交记录
	- `git log --oneline` ，只显示版本号前七个数字
- 文件恢复
	- `git restore 文件名`
- 重置
	- `git reset --hard 版本号 ` 重置某一次操作
- 还原
	- `git revert 版本号`
- 分支
	- `git branch 分支名`
	- `git branch -v` 查看所有分支
	- `git checkout 分支名` 切换分支
	- `git checkout -b 分支名` 切换并创建分支
	- `git branch -d 分支名` 删除分支
	- `git merge 分支名` 分支合并（到当前分支）
	- 若文件冲突，则修改后重新提交
- 标签
	- `git tag 标签名 版本号` ，等同于给操作起别名
-  远程仓库
	- 在`.git\config` 中的`[remote "origin"]` 中的url是远程仓库的地址
	- `git push origin` ，提交到远程仓库
	- `git pull origin`，将远程仓库下载到暂存区
	- `git remote add origin`，添加远程仓库
	- `git remote rename 名称`(将origin重命名)
	- SSH安全认证（gitee）
		- `ssh-keygen -t rsa -C远程仓库地址`
		- 查看安全证书文件的公钥（`\User\.ssh\id_rsa.pub`）
		- 在gitee的SSH公钥中添加公钥
	- 