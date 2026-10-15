# 科研工具

> 科研工具的分类清单 + 各工具的配置文件与说明。
> 这里不追求把所有工具都列全，只记录**本组实际在用、且踩过坑的**。
> 维护人：童维华｜最后更新：2026 年 10 月 15 日

---

## 一、科研工具分类

### 1. 信息搜索平台

| 平台 | 用途 | 备注 |
| --- | --- | --- |
| Google Scholar | 英文文献检索、引文追踪 | 需要能访问 |
| 知网 / 万方 / 维普 | 中文文献、学位论文 | 用校园网或校内 VPN |
| arXiv | 预印本，计算机领域一手进展 | 更新最快 |
| IEEE Xplore / ACM DL / ScienceDirect | 期刊与会议全文 | 校内 IP 通常已授权 |
| Connected Papers | 可视化文献脉络，找相关研究 | 入门某领域时很好用 |
| GitHub | 找开源实现、复现基线 | 检索用 `stars:>500` 等语法 |

### 2. AI 工具

| 工具 | 用途 | 使用边界 |
| --- | --- | --- |
| 通用大模型 | 概念解释、思路梳理、代码调试 | **不得直接生成论文正文** |
| AI 编程助手（Copilot / 通义灵码等） | 代码补全、报错解释 | 生成的代码必须自己读懂 |
| 翻译工具（DeepL 等） | 英文文献阅读辅助 | 专业术语需人工核对 |
| AI 文献工具（Consensus 等） | 根据问题检索文献 | 结果需回溯原文核实 |

> ⚠️ **AI 使用红线**：可以用 AI 查资料、理思路、改语言；**不能用 AI 直接写章节正文**。

### 3. 文献管理工具

| 工具 | 说明 |
| --- | --- |
| **Zotero** | 本组统一使用，免费、开源、支持插件 | → [Zotero.md](./Zotero.md) |
| Zotero Connector | 浏览器插件，一键抓取文献条目与 PDF |
| 茉莉花（Jasminum） | 抓取知网、万方中文文献元数据 |
| zotero-pdf-translate | PDF 划词翻译 |

### 4. IDE 与编程环境

| 工具 | 说明 |
| --- | --- |
| **VS Code** | 本组统一 IDE | → [VS Code.md](./VS%20Code.md) |
| **Python（Miniconda）** | 环境与包管理 | → [Python.md](./Python.md) |
| Jupyter | 交互式数据分析，装 VS Code 插件即可 |
| PyCharm | 新手友好，可选 |

### 5. 论文写作工具

| 工具 | 说明 |
| --- | --- |
| Markdown | 正文写作格式，本组统一 |
| Pandoc | Markdown 转 Word、PDF |
| 学年论文 Word 模板 | pandoc  `--reference-doc` 用的样式模板 | → [04-论文写作规范](../04-writing-guide/) |
| LaTeX | 公式密集时可选，一般不需要 |
| Overleaf | 在线 LaTeX，协作场景用 |

### 6. 绘图工具

| 工具 | 用途 |
| --- | --- |
| Matplotlib / Seaborn | 实验结果图（折线、柱状、混淆矩阵等） |
| Origin | 论文级统计图，部分学科更认可 |
| draw.io / Excalidraw | 流程图、模型结构图 |
| PowerPoint | 答辩 PPT、示意图拼版 |
| Figma | 界面原型（人机交互方向常用） |

### 7. 版本管理与协作

| 工具 | 说明 |
| --- | --- |
| Git | 版本管理 |
| GitHub | 本组仓库托管，组织名 `NWU-HCI-Lab` |
| GitHub Desktop | 图形化 Git，可选 |

### 8. 数据处理专用（按方向）

| 方向 | 工具 |
| --- | --- |
| EEG 情绪识别 | MNE-Python、scikit-learn |
| 面部视频情绪识别 | OpenCV、MediaPipe / dlib |
| LLM 情绪陪伴 | OpenAI / 国内大模型 API、Prompt 管理 |

---

## 二、本目录文件说明

```
02-tools/
├── README.md          ← 本文件，工具分类总览
├── VS Code.md         ← VS Code 安装与插件配置
├── Python.md          ← Python 环境与 IDE 选型
├── Zotero.md          ← Zotero 安装与翻译插件
└── images/            ← 上面几份文档的配图
```

---

## 三、安装顺序建议

```
1. VS Code        ← 一切的基础
2. Miniconda      ← 体积大，先跑起来
3. Zotero + Connector
4. 各方向专用库   ← 按你的方向装
```

---

## 四、维护说明

新增工具时请补充：工具名、用途、本组是否在用、配置文件链接。

**不要为了分类完整而列一堆没用过的工具** —— 这份清单的价值在于"用过、可靠"，不在于"全"。
