<div align="center">

# 🌿 Git 学习笔记  
### —— 从 `.git` 入门到多仓库管理  
🧭 *作者：芝士苹果派（itspommejava）*  
📅 *学习日期：2025-11-09*

</div>

---

## 🧩 一、仓库的灵魂：`.git`

> `.git` 是 Git 的「大脑 🧠」，存在于项目根目录中，用于记录所有版本、提交（Commit 提交）与远程仓库（Remote 远程）信息。

D:\java-github\java-study
│
├─ .git ← ⚙️ Git 的隐藏目录（存放版本历史）
├─ day
│ ├─ day1
│ ├─ day2
│ └─ README.md
└─ README.md

yaml
复制代码

⚠️ **不要删除 `.git` 文件夹！**  
否则仓库会“失忆”，GitHub Desktop 将无法识别它。

---

## 🗂️ 二、项目结构推荐

> 每天一个文件夹，笔记独立清晰：

day/
├─ day1/
│ └─ README.md
├─ day2/
│ └─ README.md
└─ ...

yaml
复制代码

💡 每个 `dayX` 文件夹里放一个 `README.md` 文件，  
GitHub 打开时会自动展示内容。

---

## 📁 三、空文件夹与 `.gitkeep`

> Git 不追踪空文件夹（Empty folder 空文件夹），所以如果你创建了空的 day2 文件夹，是无法 Push（推送）上去的。

✅ 解决方法之一：
day2/.gitkeep

复制代码

✅ 或直接放一个 README 文件：
day2/README.md

yaml
复制代码

> `.gitkeep` 是一种约定俗成的文件名（只是个空文件），用于“占位”。

---

## ✏️ 四、重命名与移动规则

| 操作 | 是否可行 | 说明 |
|------|-----------|------|
| 改文件夹名（例如 day1 → daystudy1） | ✅ | 改完后 Commit（提交）+ Push（推送）即可 |
| 移动整个项目文件夹 | ✅ | 只要 `.git` 一起带走就没问题 |
| 删除 `.git` 文件夹 | 🚫 | 仓库将失效 |
| 新建 `.git` | ⚠️ | 会变成新的独立仓库，不再关联 GitHub |

🪶 **小结：**  
改名和移动都没关系，只要 `.git` 在，就能继续使用。

---

## 👀 五、显示隐藏文件夹 `.git`（Windows）

1. 打开仓库文件夹  
2. 菜单栏选择「查看（View）」  
3. 勾选「隐藏的项目（Hidden items）」  
4. `.git` 文件夹就会显示出来（半透明状态）

---

## ⚙️ 六、日常操作流程

| 步骤 | 动作 | 工具 |
|------|------|------|
| ① 修改内容 | 在本地文件夹中更新代码或笔记 | 资源管理器 |
| ② Commit（提交） | 填写说明并点击 **Commit to main（提交到主分支）** | GitHub Desktop |
| ③ Push（推送） | 点击 **Push origin（推送到远程）** | GitHub Desktop |
| ④ 查看效果 | 打开 GitHub 网页仓库查看更新 | 浏览器 |

> 💬 记住：  
> 本地修改 → Commit（提交） → Push（推送）  
> 就是你的 Git 日常三步曲 🎵

---

## 🌿 七、管理多个仓库与 Push（推送）到不同远程

> 有时你会同时管理多个仓库（Repository 仓库），或希望把同一份内容推送到不同远程（Remote 远程）。  
> 这一节教你如何在 GitHub Desktop（图形界面）或命令行（git CLI）下安全管理。

---

### 🧭 1. 在 GitHub Desktop 中管理多个仓库（推荐日常做法）

#### ✅ 思路
每个仓库都是独立的——有自己专属的 `.git` 与远程地址（Remote）。  
只要在 GitHub Desktop 左上角切换仓库名称，就能分别提交和推送。

#### ✅ 操作步骤
1. 在 GitHub 上创建一个新仓库（如 `git-study`）。  
2. 在本地保留两个仓库目录：
D:\java-github\java-study
D:\java-github\git-study

yaml
复制代码
3. 打开 GitHub Desktop → `File → Clone repository...（克隆仓库）`  
克隆 `git-study` 到本地。  
4. 打开或复制文件到 `git-study` 文件夹中。  
5. 填写 **Summary（提交说明）** → 点击 **Commit to main（提交到主分支）** → **Push origin（推送到远程）**。

> ✅ 每个仓库都是独立绑定的，互不影响。

| 当前仓库 | Push（推送）到 |
|-----------|----------------|
| java-study | https://github.com/itspommejava/java-study.git |
| git-study | https://github.com/itspommejava/git-study.git |

---

### 🧠 2. 在命令行中添加第二个远程（进阶技巧）

如果你想让同一个仓库同时推送到两个远程，比如 `origin` 和 `backup`：

```bash
# 进入本地仓库目录
cd "D:\java-github\java-study"

# 添加第二个远程
git remote add backup https://github.com/itspommejava/git-study.git

# 查看远程仓库列表
git remote -v

# 推送到原始远程（origin）
git push origin main

# 同步推送到第二个远程（backup）
git push backup main
💡 backup 是你给第二个远程起的名字，可以自定义。
以后执行 git push backup main 就能同步备份。

🧾 3. 改绑（更换）远程仓库
如果你想把一个本地仓库的绑定改为另一个远程仓库：

bash
复制代码
# 修改 origin 的远程地址
git remote set-url origin https://github.com/itspommejava/new-repo.git

# 验证是否修改成功
git remote -v

# 正常推送
git push origin main
⚠️ 4. 注意事项与常见问题
项目	注意点
.git 必须保留	这是仓库核心，不可删除
不带 .git 的文件夹	不是仓库，GitHub Desktop 不识别
Desktop 不能直接添加多个 remote	需命令行操作
分支（branch）名要一致	main 分支推送时要对应
权限问题	若 Push（推送）失败，检查 GitHub 登录或 token
强制推送（force push）	慎用，会覆盖远程历史
移动仓库目录	.git 必须一起带走
新仓库初始化	用 File → Clone repository... 最安全

🪶 5. 建议的学习者工作流
步骤	动作	工具
① 编辑内容	在本地更新笔记文件	资源管理器
② Commit（提交）	写提交说明并保存版本	GitHub Desktop
③ Push（推送）	上传至主仓库（origin）	GitHub Desktop
④ 备份推送	命令行执行 git push backup main	命令行
⑤ 查看同步	打开两个 GitHub 仓库验证	浏览器

🧩 这样你就可以同时管理「学习笔记仓库」和「备份仓库」，安全又整洁。

🌸 八、今日收获总结
🪄 关键词：

.git、隐藏文件夹、Push（推送）、Commit（提交）、多仓库、Remote（远程）、Backup（备份）

🧠 今日掌握：

明白 .git 是 Git 的核心文件夹

学会了查看隐藏文件与项目结构管理

理解空文件夹无法上传的原因

掌握重命名与移动仓库规则

能独立操作多个仓库、切换并 Push（推送）

会使用命令行添加多远程（Remote）

<div align="center">
✨ 只要 .git 在，仓库就在。
✍️ By 芝士苹果派
💬 “代码与笔记，都是时间的轨迹。”

</div> ```