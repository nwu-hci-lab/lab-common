# 新人入门指南

> 赵健老师课题组，由我（童维华）带大家做学年论文。
> 这份文档的目标很简单：**一周之内，你能自己提交、能发 PR、能看懂我留的批注。**
> 维护人：童维华｜最后更新：2026 年 10 月 15 日

---

## 0. 要做到什么程度

不用精通 Git，也不用背命令。你只要能稳定做到下面六件事就行：

| 能力 | 命令 |
| --- | --- |
| 把仓库下到自己电脑 | `git clone` |
| 同步别人最新的改动 | `git pull` |
| 看自己改了什么 | `git status` / `git diff` |
| 把改动存成一个记录点 | `git add` + `git commit` |
| 把记录点传上 GitHub | `git push` |
| 叫我来看 | 发起 Pull Request |

**过关标准**：不看文档，自己走一遍「改文件 → 提交 → 推送 → 发 PR」。

---

## 1. 先把环境装好（第一天花一小时）

### 1.1 装 Git

**Windows**（大部分同学）

去 [Git for Windows](https://git-scm.com/download/win) 下载，一路 Next 默认装完。

装完之后，开始菜单里搜 **Git Bash**，之后所有命令都在它里面敲。别用 cmd 和 PowerShell——教程里的命令在它们身上会出各种莫名其妙的问题，没必要给自己找麻烦。

**macOS**

打开终端敲 `git --version`，会顺带弹出 Xcode 命令行工具的安装提示，装上就好。

**Linux**

```bash
sudo apt install git
```

装完敲 `git --version`，能出版本号就成功了。

### 1.2 装 VS Code

论文和代码都用它写：[VS Code](https://code.visualstudio.com/)。左边那个分叉图标就是 Git 面板，你改了哪几行一眼能看到。

建议装两个插件：**GitLens**（能看到每一行是谁什么时候改的）、**Markdown Preview Enhanced**（写论文时右边实时预览）。

### 1.3 进组织

1. 注册 GitHub 账号。用户名用真名拼音，比如 `tongweihua`。别用 `coolboy520` 这种，我在几十个仓库里认不出你是谁。
2. 把用户名发给我，我发邀请。
3. 收到邀请后**当天**去邮箱点接受，邀请会过期，过期了我得重发。

### 1.4 配置身份

这一步漏了的话，你的提交不会算到你头上，我这边看到的是一串陌生名字。

```bash
git config --global user.name  "张三"
git config --global user.email "zhangsan@example.com"
```

邮箱必须和你注册 GitHub 用的那个**完全一样**。

### 1.5 配 SSH 密钥

配好了以后 push 不用每次输密码。这是全文最容易卡住的一步，照着抄别自己发挥。

**生成密钥**（邮箱换成你自己的）：

```bash
ssh-keygen -t ed25519 -C "zhangsan@example.com"
```

一路回车，不要设密码。

**看公钥并复制**：

```bash
cat ~/.ssh/id_ed25519.pub
```

输出是一长串 `ssh-ed25519 AAAA...` 开头的东西，从开头到你的邮箱，**整段复制**。

**贴到 GitHub**：

右上角头像 → Settings → SSH and GPG keys → New SSH key → Title 写你电脑名（比如"张三-笔记本"），Key type 选 **Authentication Key**，粘进去 → Add SSH key。

**验证**：

```bash
ssh -T git@github.com
```

看到 `Hi 你的用户名! You've successfully authenticated...` 就成了。第一次会问 `Are you sure you want to continue connecting?`，输 `yes` 回车。

卡超过半小时就别死磕，截图开个 Issue，我远程帮你看。

### 1.6 网络问题

国内访问 GitHub 确实时好时坏。`clone` 或 `push` 超时的话：

- 先重试一次，很多时候就是抽风
- 一直不行就在 Issue 里说一声，我给你加速方案
- 别因为连不上就改成微信发我文件。绕开一次，后面就一直想绕。

---

## 2. 第一次提交，跟着走一遍

假设你要往 `lab-common` 里交一篇文献笔记。

```bash
# ① 下载仓库，只要做一次
git clone git@github.com:NWU-HCI-Lab/lab-common.git
cd lab-common

# ② 开工前先同步（每次干活前都做）
git pull

# ③ 用 VS Code 编辑文件
#    比如新建 03-组会与文献分享/2026-10-20-张三-EEG情绪识别综述.md

# ④ 看看自己动了什么
git status        # 红色 = 改了还没存成记录点
git diff          # 看具体改了哪几行

# ⑤ 加入暂存区
git add 03-组会与文献分享/2026-10-20-张三-EEG情绪识别综述.md

# ⑥ 存成记录点
git commit -m "文献: 新增 EEG 情绪识别综述笔记"

# ⑦ 传上去
git push
```

刷一下 GitHub 网页，能看到你的文件和提交记录。第一次提交完成。

---

## 3. 日常怎么用

### 开工前

```bash
git pull
```

新手最常犯的错就是不 pull 直接动手。别人改了你没同步，等你 push 的时候就冲突，解冲突比重写还难受。

### 收工前

```bash
git status                 # 确认没漏文件
git add .                  # 加入改动
git commit -m "阶段: 动作"   # 提交
git push                   # 推送
```

**每天都 push 一次**，哪怕只写了两百字。三个原因：

一是硬盘坏了不丢东西，GitHub 就是你的云备份；二是我能看到你的真实进度，而不是最后一天突然冒出来一个大文件；三是断断续续的小提交才像正常的写作过程——憋一周丢上来一万字，我只能当 AI 代写来问你。

### 命令速查

| 命令 | 作用 | 什么时候用 |
| --- | --- | --- |
| `git clone <地址>` | 下载仓库 | 第一次 |
| `git pull` | 拉最新改动 | 开工前 |
| `git status` | 看改了哪些文件 | 随时 |
| `git diff` | 看改了哪几行 | 提交前自检 |
| `git add <文件>` | 加入暂存区 | 提交前 |
| `git commit -m "说明"` | 存成记录点 | 完成一个小改动 |
| `git push` | 传到 GitHub | 收工前 |
| `git log --oneline` | 看历史提交 | 想回看时 |
| `git checkout -- <文件>` | 撤销未提交的改动 | 改坏了重来 |

`git add .` 里的 `.` 是"所有文件"的意思。提交前先 `git status` 看一眼，别把下载的数据集、临时文件一起加进去。

---

## 4. 分支和 PR

### 为什么不能直接改

组织的 `main` 分支是锁着的，你推不上去。所有改动都要走：

```
你的分支 → 发 PR → 我看 → 我合并进 main
```

这样 `main` 上的东西永远是我看过的、能用的。

### 怎么操作

```bash
# ① 新建并切到自己的分支，分支名写清楚在干什么
git checkout -b thesis/张三-第三章初稿

# ② 正常改、正常提交
git add .
git commit -m "初稿: 完成第三章方法部分"
git push -u origin thesis/张三-第三章初稿
#                                            ↑ 第一次推新分支要加 -u

# ③ 打开 GitHub，会看到黄色提示条，点 Compare & pull request
#    Title 写：初稿: 完成第三章方法部分
#    Body 写：改了什么、还有什么问题、希望我重点看哪里
```

### 发完 PR 之后

- 我会在具体行上留批注
- 你照着改，**继续在同一个分支上 commit 然后 push**，PR 会自动更新，不用重新开一个
- 我点 Merge，这阶段就算过了
- 合并完切回主干继续下一轮：`git checkout main && git pull`

### 分支怎么起名

| 类型 | 格式 | 例子 |
| --- | --- | --- |
| 论文阶段 | `thesis/姓名-内容` | `thesis/张三-文献综述` |
| 代码功能 | `feat/功能名` | `feat/eeg-preprocessing` |
| 修 Bug | `fix/问题描述` | `fix/采样率错误` |
| 文档 | `docs/文档名` | `docs/更新入门指南` |

---

## 5. 提交信息怎么写

格式就一条：`阶段或类型: 做了什么`。

```
好的：
文献: 新增 DEAP 数据集相关研究笔记
提纲: 调整第三章结构，合并 3.2 与 3.3
初稿: 完成第四章实验结果分析
代码: 修复 EEG 滤波参数错误
文档: 补充 SSH 配置常见问题

不好的：
更新 / 修改 / 123 / aaaa / final / final2 / 真的是final
```

期末我 `git log` 一翻，好的提交信息就是你的工作日志；写"更新"等于没留记录，三个月后你自己都想不起来当时干了啥。

---

## 6. 报错了先看这儿

| 报错 | 原因 | 怎么办 |
| --- | --- | --- |
| `Permission denied (publickey)` | SSH 没配对 | 重做 1.5，注意公钥要整段复制 |
| `failed to push some refs` | 本地落后了 | 先 `git pull` 再 `git push` |
| `CONFLICT (content)` | 和别人改了同一行 | 别慌，更别 force push，开 Issue 找我 |
| `src refspec does not match` | 分支名写错 | `git branch` 看真实分支名 |
| `LF will be replaced by CRLF` | Windows 换行符警告 | 不是错误，无视 |
| `Filename too long` | Windows 路径长度限制 | `git config --global core.longpaths true` |
| 中文文件名显示成 `\344\275\240` | Git 转义了非 ASCII | `git config --global core.quotepath false` |

实在不行：复制完整报错 → 开 Issue → 等我的时候可以自己拿报错去搜一下，大概率能搜到。

---

## 7. 各自的节奏

### 大一同学：四天通关

| 时间 | 干什么 | 怎么算过 |
| --- | --- | --- |
| 第 1 天 | 装环境、配 SSH、clone 仓库 | `ssh -T git@github.com` 出成功提示 |
| 第 2 天 | 在 `lab-common` 交一篇文献笔记 | 网页上能看到你的提交 |
| 第 3 天 | 学会分支，发第一个 PR | PR 页面出现，我收到通知 |
| 第 4 天 | 按我的批注改完再提交 | PR 被合并 |

第一周过后，你只需要记住五个命令：`pull → status → add → commit → push`。

### 大三同学：两天，另外多几点要求

基础部分自己搞定，一小时够了。在此之上还要会：

- 用 `git diff` 读懂差异，提交前自己先 review 一遍
- 明白冲突是怎么产生的，能处理基本的，别只会开 Issue
- 给大一同学的 PR 做一次同行评审
- 在 `lab-common/05-踩坑记录/` 里至少沉淀一篇踩坑文档

说句实在的：大三会用 Git 不算加分项，是应该的。能把大一同学带起来，才是你这学期要考核的东西。

### 有余力再看

`git stash`（临时存起改动）、`git rebase -i`（整理提交历史）、`git cherry-pick`（挑某个提交）、`git log --graph`（看分支图）。

---

## 8. 第一周自测清单

逐项打勾，把这个清单截图发到你的第一个 Issue 里。

- [ ] Git 装好了，`git --version` 有输出
- [ ] VS Code 装好了
- [ ] 组织邀请已接受，能看到仓库
- [ ] `user.name` 和 `user.email` 配好了，邮箱和 GitHub 一致
- [ ] SSH 配通了，`ssh -T git@github.com` 出欢迎信息
- [ ] `lab-common` 已经 clone 到本地
- [ ] 第一篇文献笔记已提交并 push 成功
- [ ] 第一个 PR 发出来了
- [ ] `../04-论文写作规范/` 下的文档读完了

---

## 9. 几条硬规矩

1. **每周 push。** 提交记录既是你的工作日志，也是你唯一的备份。
2. **不许 force push `main`。** 犯一次，这学期的过程记录就作废了。
3. **有事开 Issue。** 卡住了、要请假、想换题，都开 Issue，别只发微信。微信会沉底，Issue 不会。

---

## 怎么问我问题

1. 先搜这份文档和相关仓库的 README
2. 再去对应仓库开 Issue，**带上完整报错截图**
3. 真着急再私聊我

别跟我说"我 push 不上去"，跟我说"我执行 `git push` 报了 `Permission denied (publickey)`，截图在这里，1.5 节我做过一遍，卡在第 X 步"。前一种我得追问三轮，后一种一轮就解决。
