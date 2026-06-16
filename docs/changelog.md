# 更新日志

> 本日志以**用户视角**记录功能变化，遵循 [Keep a Changelog](https://keepachangelog.com/zh-CN/1.1.0/) 格式。
> 详细技术变更与代码 commit 请到 [GitHub Releases](https://github.com/EgoMatrix/XImage/releases) 查看。
>
> 版本号遵循 [Semantic Versioning](https://semver.org/lang/zh-CN/)：`主版本.次版本.修订号`。

---

## [Unreleased]

> 本节用于汇总下一版还未发布的内容，发版时整理进对应版本号。

### 新增
- _暂无_

### 优化
- _暂无_

### 修复
- _暂无_

---

## [0.0.8] - 2026-06-16

围绕发布同步链路的小幅强化，让公开仓的源码层（main 分支）也能始终拿到与最新 Release 一致的 `docs/changelog.md`，便于用户在仓库主页直接查看历史变更。

### 新增

- **changelog 文件级同步**：`release-sync` workflow 在创建公开仓 Release 之前，新增「Sync Changelog File to Public Repo Codebase」步骤——浅克隆公开仓 main 分支，将私有仓最新的 `docs/changelog.md` 覆盖过去并提交，commit message 自动带上当前 tag。无变更时自动跳过，不会产生空提交。

### 优化

- 公开仓 Release 创建时显式指定 `--target main`，避免在初始仓库（尚未有用户态代码）状态下创建 Release 时出现挂载异常。

---

## [0.0.7] - 2026-06-16

本版聚焦**发布工程**与**创作体验**两条线：补齐了公开仓所需的全部用户文档、把私有仓制品自动同步到公开仓的链路打通；同时新增「创意概念」创作模式，并细致打磨了多个字段与首页布局。

### 新增

#### 创作工作台
- **新增「创意概念」创作模式**：覆盖 mini-me / 巨人国 / 真人 + 卡通混搭 / 双重曝光 / 漂浮失重 / 被卷入海报或屏幕 / 电影分镜动作 / 超现实物理等 12+ 概念，专为戏剧感画面与广告大片打造。
- **创作分类切换改为胶囊式 tab**：一行展示 9 个模式，整体更干净，避免在窄屏下换行错位。

#### 公开仓发布体系
- 新增 `README-public.md`：用户视角的公开仓首页，含三平台下载入口、九大模式速览、隐私说明。
- 新增 `LICENSE-DOCS`：文档采用 CC-BY-4.0、软件保留所有权利的双授权声明。
- 新增 `docs/user-guide.md`：完整用户手册（11 节），含「渠道与三类模型（必读）」入门章节、5 分钟跑通指引、九大模式逐一讲解、AI 策划与参考图用法、FAQ 速查。
- 新增 `docs/faq.md`：覆盖安装、渠道、模型、参考图、隐私、bug 反馈等高频问题。
- 新增 `.github/ISSUE_TEMPLATE/`：bug 报告 / 功能建议 / 渠道与模型支持三套 issue 表单。

#### 发布同步链路
- 新增 `.github/workflows/release-sync.yml`：监听构建 workflow 完成后自动接力，把私有仓 Release 中的安装包按白名单同步到公开仓 `EgoMatrix/XImage` 的同名 Release。
- 同步流程内置 `checksums.txt` 自动校验、SHA256 摘要审计、Release Notes 自动从 changelog 抽取。
- 提供本地兜底脚本 `scripts/release-sync.sh` 与 `scripts/sync-public-docs.sh`，配合 `extract-changelog.py` 让 docs 与制品都可手动跑通同步流程。

### 优化

#### 字段交互
- **表情包「核心情绪 / 表情文字」**：由单行文本改为 textarea，与右侧候选 chips 等高，多行内容不再被截断。
- **海报物料「目标人群」**：同步改为 textarea，最大长度上调到 120。
- **自由创作「情绪氛围」**：同步改为 textarea，最大长度上调到 100。
- 用户文档「渠道与模型」一章重写为傻瓜式：先给「OpenAI 一家全包」最简路径，再列「想省钱 / 换花样」的常见组合，三句话总结收尾。

#### 首页布局
- **预览大图与「更多候选」固定 20px 间距**：不再因左列「生成参数」高度变化或比例切换出现大段空白。
- 预览框宽高比改为跟随真实图像或当前比例，3:4 与 16:9 切换不再被旧图卡住。

### 修复
- `release-sync` workflow 中 `gh release view` 误写、参数解析与 mac bash 3.x 关联数组兼容问题修复，现已端到端跑通同步全流程。
- 修复创作分类 tab 在窄屏下换行错位的问题。
- 修复 textarea 与右侧 chips 列表存在轻微高度漂移的问题。

---

## [1.0.0] - 2026-06-15

XImage 首个正式版本，覆盖完整 MVP 功能。

### 新增

#### 核心生图工作台
- 全新「**生图工作台**」：左侧创作参数、右侧预览效果与候选图，桌面双列布局自适应。
- **九大创作模式**：
  - 内容封面（小红书 / 公众号 / 抖音 / 视频号 …）
  - 人物角色（设定表、转身、表情、姿态、头像）
  - 商品素材（主图、详情、种草、包装、品牌物料）
  - 场景设定（空间、世界观、镜头）
  - 海报物料（活动、品牌、课程、节日）
  - 特效素材（光效、粒子、烟雾、HUD，25+ 子类）
  - 表情包（单张 / 四宫格 / 九宫格 / 贴纸套组 / 梗图）
  - 创意概念（mini-me / 巨人国 / 双重曝光 / 漂浮失重等 12+ 概念）
  - 自由创作
- **AI 提示词策划助手**：把字段组装为原始提示词，再由 LLM 优化为可执行提示词，自动给出风格、构图、负面词建议。
- **完整提示词编辑器**：可手工改写优化提示词与负面词，支持「重新生成」。
- **参考图（图生图）**：支持 1 ~ 4 张参考图，自动识别并切换到 remix 模型。

#### 渠道与模型管理
- 三类渠道支持：OpenAI 官方、中转 API、自定义 Base URL。
- 渠道字段：名称、类型、Base URL、API Key、代理、超时、启用状态、默认渠道。
- 渠道能力：planning（提示词优化）/ generation（文生图）/ remix（图生图）。
- 模型管理：预置常见模型（GPT-Image 系列、Google Imagen、字节、MiniMax、Kimi 等），并支持「新增自定义模型 ID」。
- 一键测试连接、查看渠道可用模型列表。

#### 生图记录
- 历史网格：按提示词 / 模型 / 渠道 / 时间筛选与搜索。
- 大图查看、原始与优化后提示词对照、渠道与模型元数据。
- 一键「重新生成」复用提示词。
- 一键「保存到本地」与「打开文件夹」。

#### 设置与隐私
- API Key 本地加密存储，**不**上传任何服务器。
- 数据全部存储在用户本地目录，支持整体迁移。
- 调用日志：每次接口调用的请求参数与错误响应可在「设置 → 调用日志」查看。
- 默认保存路径、参考图数量上限、默认渠道等可配置。

#### 安装与平台
- macOS（Apple Silicon / Intel）`.dmg` 安装包。
- Windows 64 位 `.exe` 安装包。
- Linux `.AppImage` 单文件运行。

### 文档
- 公开仓 `README.md` + `docs/user-guide.md`（完整用户手册）+ `docs/faq.md`（常见问题）。
- 飞书详尽版用户指南（含截图与视频）。

---

[Unreleased]: https://github.com/EgoMatrix/XImage/compare/v0.0.8...HEAD
[0.0.8]: https://github.com/EgoMatrix/XImage/releases/tag/v0.0.8
[0.0.7]: https://github.com/EgoMatrix/XImage/releases/tag/v0.0.7
[1.0.0]: https://github.com/EgoMatrix/XImage/releases/tag/v1.0.0
