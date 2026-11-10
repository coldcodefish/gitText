# 初学git

## init

现在AI真方便，之前没有“科学上网”，初学的时候，也没有需求，
git的学习就中断了，后面有了“魔法”之后，短时间要突然需要，
用AI调用git帮忙，就又有了git的需求，就又开始git的学习了。

## 内容说明

git相关的代码，及其他各种杂代码

教程来自与：https://blog.csdn.net/2301_79448707/article/details/158977213

## git命令

### 信息初始化

git config --global user.name "xxx"                       # 配置用户名
git config --global user.email "xxx@xxx.com"              # 配置邮件

### 设置 Git 代理(proxy)

<!-- HTTP/HTTPS 协议，port 需与代理软件设置的一致 -->
git config --global http.proxy http://127.0.0.1:port      # 注意修改 port
git config --global https.proxy http://127.0.0.1:port
<!-- 瓦特工具箱为127.0.0.1:7890 -->

### 取消 Git 代理

<!-- 当你处于无需代理的网络环境时，应取消代理设置，否则可能导致无法连接： -->
git config --global --unset http.proxy
git config --global --unset https.proxy

###  生成本地 SSH 密钥

<!-- 打开终端，输入以下命令（注意替换成你自己的邮箱）： -->
ssh-keygen -t ed25519 -C "你的邮箱@example.com"

### 查看并复制生成的公钥 

1. 打开电脑的文件管理器。
2. `C:\Users\你的用户名\.ssh\` 文件夹。
3. 名为 id_ed25519.pub 的文件，右键纯文本打开它。

### 将公钥添加到 GitHub

1. 登录 GitHub，点击右上角头像 -> Settings。
2. 左侧菜单找到 SSH and GPG keys，点击 New SSH key。
3. Title 随便填（用来标记这台电脑，如 My Laptop 或 公司电脑）。
4. 在 Key 输入框中，粘贴你刚刚在 2.2 步复制好的那一长段公钥内容。
5. 点击 Add SSH key 完成添加。

### 克隆已有项目（接手代码）
1. 按下 F1 或 Ctrl + Shift + P 打开命令面板。
2. 输入 Git: Clone 并回车。

### 推送 (Push)
<!-- 如果你是场景一（本地新建），首次推送需要先关联 GitHub： -->
git remote add origin 你的GitHub仓库链接
git push -u origin main                                    # 首次推送并绑定分支

### 拉取 (Pull)
<!-- 如果是团队协作，或者你在另一台电脑上修改了代码，修改本地代码前必须先拉取云端最新代码。 -->
git pull

### 分支操作 (Branch)
1. 查看所有分支
    git branch
2. 创建并直接切换到新分支 (极常用)
    git checkout -b feature-login
3. 切换回主分支
    git checkout main

### Git 的“后悔药”（撤销与回退）
<!-- 写错代码或者提交错了怎么办？记住以下几个最常用的回退场景： -->

1. 场景一：代码写崩了，想恢复到上一次提交的状态
    还没执行 git add，想直接丢弃工作区的修改。

- 界面操作：在“源代码管理”中找到那个文件，点击右侧的 “撤销更改” (弯曲的返回箭头)。
- 命令行操作：git restore <文件名> （丢弃所有修改用 git restore .，慎用！）

---

2. 场景二：不小心点了 + 号暂存，想撤回
    执行了 git add，但还没 commit。

- 界面操作：在“暂存的更改”列表中，点击文件右侧的 - 号（取消暂存）。
- 命令行操作：git restore --staged <文件名>

---

3. 场景三：提交完了，发现漏了东西或写错备注
    已经 commit 了，代码不想丢，只是想撤销这条 commit 记录。

- 界面操作：点击 “…” -> 提交 -> 撤销上次提交 (Undo Last Commit)。你的代码会原封不动地回到暂存区。
- 命令行操作：git reset --soft HEAD^

---

4. 场景四：彻底不要上次的提交了（核弹级命令⚠️）
    连提交记录带修改的代码全部清空，彻底回到上一个版本。

- 命令行操作：git reset --hard HEAD^

---

5. 场景五：强行用本地覆盖云端（核弹级命令⚠️）
    你的本地代码是正确的，但云端乱了，需要强行同步。

- 命令行操作：git push origin main -f
 <!-- -f 即 --force（强制）。团队协作绝对不要用（会被同事追杀）；个人项目用起来很爽。 -->
