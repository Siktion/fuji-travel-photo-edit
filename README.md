# Fuji Travel Photo Edit

一个面向 Codex 的照片修图 Skill，源自富士旅行照片、人像精修、批量编辑与创意风格处理经验。默认按纪实保真方式修图：改善照片观感，同时保留真实场景、人物身份和原片信息。

## 适用场景

- 富士 JPG 的曝光、白平衡、局部明暗、构图和肤色调整。
- 用户明确指定的人像局部精修或轮廓修饰。
- 用户明确指定的创意风格编辑，并将生成式重绘与普通调色区分开。
- 单张或批量处理，包括来源映射、输出检查和交付记录。

照片快剪由 `photo-beat-montage` Skill 负责。RAF 内嵌预览不等于 RAW 显影；低分辨率生成结果不等于原尺寸母版。

## 安装

把整个仓库目录安装到 Codex 的 Skills 目录：

```sh
mkdir -p "$HOME/.codex/skills"
git clone https://github.com/Siktion/fuji-travel-photo-edit.git \
  "$HOME/.codex/skills/fuji-travel-photo-edit"
```

如果目录已经存在，先备份本地修改，再更新：

```sh
git -C "$HOME/.codex/skills/fuji-travel-photo-edit" pull --ff-only
```

也可以把仓库目录复制到项目的 `.agents/skills/fuji-travel-photo-edit/`，让 Skill 随项目使用。安装后在新任务中调用；若 Codex 尚未发现它，重启或刷新 Skill 列表。

## 使用

在 Codex 中明确调用 `$fuji-travel-photo-edit`，并说明素材位置、编辑目标、输出目录、格式/尺寸要求和处理数量。例如：

> 使用 `$fuji-travel-photo-edit` 修整 `photos/trip/DSCF1234.JPG` 的曝光和白平衡。保留原图，结果另存到 `output/`，保留原尺寸与方向，并说明实际使用的工具和检查结果。

人像或批量处理时，补充指定人物/区域、允许改变的内容、需要保留的特征，以及逐张交付要求。先做单张样片并检查输出，再决定是否扩展到整批。

## 核心边界

- 原片只读，编辑结果写入独立目录；不移动、覆盖或删除来源文件。
- 上传个人照片到云端服务前，先列明本轮要上传的照片和目标服务，并取得用户明确同意。
- 用户指定了编辑器、API 或模型时，先核实当前确实能调用该后端且支持所需格式/尺寸；无法调用就说明未完成，不静默换用其他后端。
- 实际修图依赖当前会话可用的图像工具。Skill 提供工作流程，不会自行安装或提供修图后端。没有合适工具时，只能说明限制或给出方案，不能声称照片已经编辑。
- 真实场景与人物身份是默认不变量。瘦脸、身形调整及“魔界领域”等创意重塑，必须由用户明确提出并按相应标准验收。
- 复制原图、未生成、拒绝和未处理项分别记录，不计为已修好的照片。文件存在或可解码不能代替逐张视觉检查，也不等于用户已确认审美。

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

- [`SKILL.md`](SKILL.md)：主流程、工具路由、编辑模式和验收规则。
- [`references/editing.md`](references/editing.md)：逐图摄影后期和保真规则。
- [`references/portrait-retouch.md`](references/portrait-retouch.md)：面部细节、肤色和轮廓边界。
- [`references/batch-workflow.md`](references/batch-workflow.md)：批量筛选、来源映射、状态和交付检查。
- [`references/creative-restyle.md`](references/creative-restyle.md)：明确要求的电影化或奇幻风格重塑。
