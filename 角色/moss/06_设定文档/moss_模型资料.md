# MOSS · 模型资料（拟人对象）

> 检索日 **2026-10-28**。**这两个是角色原型（要拟人化的模型），不是我们出图的工具**——
> 出图仍按 `REFS/character-pack-workflow.md`：gpt-image-2.5 出草图 / Seedream 5.0 Flash 修图。

---

## 〇、命名来源（已核实，团队原话）

**MOSS 的取名来自《流浪地球2》里那台 MOSS（550W），不是苔藓。**

> 「与自然语言处理领域的其他一些模型一样，开发者会用自己喜欢的影视角色名称命名模型。
> 我们在训练完第一代模型的时候，正值《流浪地球2》热映，影片中的 MOSS 给团队里每个人留下了深刻印象，
> 所以用它来称呼我们开发的模型，**以表达我们对最前沿人工智能模型的不懈追求**。」
>
> —— 复旦科研团队，2023-02-22（解放日报 俞陶然，中青网转载）

- 中青报/解放日报：<http://s.cyol.com/articles/2023-02/22/content_gG9A40sz.html>
- 澎湃/新浪财经（同上口径）：<https://finance.sina.com.cn/jjxw/2023-02-21/doc-imyhmhnz5145548.shtml>

**注意**：`moss` 英文本义确实是苔藓，但**官方出处没有提苔藓**——苔藓只能算我们自己可用的第二层联想，
**写设定/发布文案时不许说成"官方寓意是苔藓"**。原模型（2023 年第一代 MOSS，160 亿参数、8×A100）
→ 现在的 MOSS-Image / MOSS-TTS 沿用这个名字。

---

## 一、MOSS-Image（生图模型）

| 项 | 事实 |
|---|---|
| 出品 | **OpenMOSS 团队 / 模思智能**（复旦邱锡鹏团队线） |
| 架构 | **5B DiT 主干**；Base + curated-data 微调版（SFT）两个权重 |
| 开源 | **2026-10-16** 放代码与权重，许可 **Apache-2.0** |
| 特色能力 | ① **原生布局控制**：JSON prompt + bounding box 指定物体/文字的位置与大小 ② 提示词最长 **4K tokens** ③ **文字渲染强** ④ 动漫与写实风格都覆盖 |
| 训练特征 | **从训练数据里剔除 AI 生成图** → 海外评价"没有 AI 味" |
| 热度 | 上线 4 天 **130 万次下载**、GitHub **1.4k stars**、登顶 HF 文生图趋势榜 |
| 衍生生态 | 8 步 / 4 步加速、INT8、**GGUF**、摄影与动漫 LoRA、ComfyUI 工作流 |
| 对标 | **FLUX.3-klein、Krea2、Qwen Image 2.1** |

- 官网：<https://openmoss.ai/MOSS-Image/>
- 报道：<https://www.qbitai.com/2026/10/504930.html>（量子位 2026-10-23）

## 二、MOSS-TTS（语音合成模型）

| 项 | 事实 |
|---|---|
| 出品 | **复旦大学 OpenMOSS 团队 + MOSI.AI** |
| 代表权重 | **`MOSS-TTS-Nano-100M`**：约 **1 亿（100M）参数** |
| 架构 | **Audio Tokenizer + LLM 自回归** |
| 亮点 | **部署优先**：**CPU 实时推理**、多语种、高保真语音设计 |
| 许可 | Apache-2.0 |
| 技术报告 | 2026-03-18 / v2 03-20，`arXiv:2603.18090` |
| 报告要点 | Tokenizer = **MOSS-Audio-Tokenizer**：因果 Transformer，**24 kHz → 12.5 fps**，变比特率 RVQ、语义与声学统一表示；两个生成器 **MOSS-TTS**（长上下文/控制导向）与 **MOSS-TTS-Local-Transformer**（帧局部自回归，效率高、**说话人保持强**、**首字延迟低**） |

- 模型页：<https://aihub.caict.ac.cn/models/OpenMOSS/MOSS-TTS-Nano-100M>
- 技术报告：<https://export.arxiv.org/abs/2603.18090>

## 三、官方视觉资产（已下载到 `_参考\`）

| 文件 | 内容 | 取处 |
|---|---|---|
| `openmoss-logo.svg` | **官方图标**：左侧蓝色 `M` 斜切字形 ＋ 右侧**方块阵列圆环**，渐变 `#3b7fe0 → #7fe6fb` | `openmoss.ai/MOSS-Image/assets/logo.svg` |
| `openmoss-lockup-light.svg` | 字标组合（logo + MOSS 字） | 同站 `assets/lockup-light.svg` |
| `openmoss-github-avatar.png` | GitHub 组织头像 | `avatars.githubusercontent.com/OpenMOSS` |
| `moss-image-teaser.webp` | 官方头图 | `assets/teaser.webp` |
| `moss-image-showcase-overview*.webp` | 官方效果展示（两张，含布局控制示意） | `assets/showcase/` |
| `moss-image-compare-base/sft.webp` | Base 与 SFT 的对比 | `assets/comparison/` |

**从 logo 读出的设计语言（重要）**：

- **品牌色 = 蓝 → 青渐变**（`#3b7fe0` 深蓝 → `#4aa5f2` → `#7fe6fb` 浅青），**不是绿色**
- 图形语言 = **圆角方块阵列**排成弧/环（方块 46.48、圆角 8.36，逐级变浅）
- 字形语言 = `M` 的一笔长斜切
- → 这三样（青蓝渐变、方块阵列、斜切 M）都能直接变成角色的发饰、裙边、悬浮粒子与剪影特征

> ⚠️ 未取到：HuggingFace 组织头像（`api/organizations/OpenMOSS/avatar` 只回 0.1 KB）。要用 F5 再试或手动存。

## 四、要用作素材时注意

- **别把 MOSS-Image 当工具**：它是拟人对象。真要拿它出图得本地部署（5B / GGUF），与角色拟人是两条线。
- 热度类数字（130 万下载 / 1.4k stars）会变，写进发布文案前**再核一次**。
