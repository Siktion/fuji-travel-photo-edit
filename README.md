# 个人照片修图 Skill

基于富士旅行照片、人像精修、批量 AI 编辑与创意风格处理记录整理的 Codex Skill。默认采用纪实保真精修；人物轮廓调整和“魔界领域”等创意重塑必须由用户明确提出，并按各自标准验收。

## 能做什么

- 修整富士 JPG 的曝光、白平衡、局部明暗、构图和肤色，保留真实场景与人物身份。
- 按明确要求进行人像局部精修或克制的轮廓修饰；目标不确定时保留原图并标记未编辑。
- 按明确风格要求制作创意编辑候选，并区分生成式重绘与普通调色。
- 规划单张或批量处理，维护来源映射、编辑状态、尺寸、检查范围和交付说明。

本 Skill 不负责照片快剪；本项目的 `photo-beat-montage` Skill 负责该流程。RAF 嵌入预览不等于 RAW 显影；低分辨率生成结果不等于原尺寸母版。

## 使用

在本项目中，读取 [`SKILL.md`](SKILL.md) 后按本轮要求执行。可用以下提示开始：

> 使用 `$fuji-travel-photo-edit` 按我指定的方向修图，保留原片并逐张核对输出。

若尚未将此目录安装到 Codex 的用户级 Skills 路径，使用上述 `$` 调用前需先安装。可将整个 `fuji-travel-photo-edit` 目录复制到 `~/.codex/skills/`；安装后重启或刷新 Codex Skill 列表。

## 文件

```text
fuji-travel-photo-edit/
├── SKILL.md
├── README.md
├── agents/
│   └── openai.yaml
└── references/
    ├── batch-workflow.md
    ├── creative-restyle.md
    ├── editing.md
    └── portrait-retouch.md
```

按需阅读：

- [`references/editing.md`](references/editing.md)：逐图摄影后期和保真规则。
- [`references/portrait-retouch.md`](references/portrait-retouch.md)：面部细节、肤色和人像轮廓边界。
- [`references/batch-workflow.md`](references/batch-workflow.md)：大目录筛选、逐图状态、映射及交付检查。
- [`references/creative-restyle.md`](references/creative-restyle.md)：明确要求的电影化/奇幻风格重塑。

## 核心处理约束

- 原片只读，编辑结果另存到新版本目录；云端处理前先取得用户同意，只上传本轮选中的照片。
- 用户指定 OpenAI Images API 等特定后端时，必须确认实际调用该后端；不可用就停止该后端任务，不以其他工具的结果替代。
- 场景、人物、方向、比例和像素尺寸都要对照原片核验。错误场景、画幅/方向不符、身份漂移和背景伪影应拒收或标为未完成。
- 原样副本、未生成、拒绝和未处理项分别计数，不算作已精修。
- 文件存在、可解码、哈希或压缩包完整只证明相应文件属性；不能代替逐张视觉复核，也不能证明用户已确认审美。
