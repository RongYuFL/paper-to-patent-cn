# Paper to Patent CN

根据论文、设计文档、代码仓库 README 等技术材料，直接撰写或修订中文发明专利申请文件的轻量 Agent Skill。

材料可以单独使用，也可以组合提供。核心技术提炼在当前任务内完成，正文撰写、现有技术研究、附图与 Word 规范按需加载。已有完整论文时优先利用其引言、相关工作、方法和实验，不默认再执行一套完整检索流程。

## 适用场景

可用于从技术材料起草完整专利稿，或者修改已有稿件的权利要求、背景技术、发明内容、实施例、摘要和附图。适用于人工智能模型与方法等技术方案，具体领域、架构和实施例由所提供材料决定。

适合通过计算机程序实现的完整稿，默认包括方法、系统、电子设备及计算机可读存储介质；用户指定范围优先。技能提供写作辅助，不承诺查新结论、专利授权或代办申请。

## 目录与按需加载

```text
paper-to-patent-cn/
├── SKILL.md
├── agents/openai.yaml
└── references/
    ├── prior-art-research.md
    ├── patent-drafting.md
    └── figures-and-docx.md
```

| 模块 | 加载条件 |
| --- | --- |
| `SKILL.md` | 任务入口、材料解析、核心技术提炼、范围控制和全局约束 |
| `prior-art-research.md` | 明确要求检索、查新、初筛，或关键背景事实缺少支持 |
| `patent-drafting.md` | 起草或修订正文，只读取相关章节 |
| `figures-and-docx.md` | 实际处理附图、图号或 DOCX |

## 安装到 Codex

下载本仓库，在仓库目录执行下面适合你系统的命令。已有同名技能时，请先保留自己的修改。

### Windows PowerShell

```powershell
$patentSkillsRoot = if ($env:CODEX_HOME) { Join-Path $env:CODEX_HOME 'skills' } else { Join-Path $HOME '.codex\skills' }
$patentSkillTarget = Join-Path $patentSkillsRoot 'paper-to-patent-cn'
New-Item -ItemType Directory -Force -Path $patentSkillTarget | Out-Null
Copy-Item -LiteralPath '.\SKILL.md' -Destination $patentSkillTarget
Copy-Item -LiteralPath '.\references', '.\agents' -Destination $patentSkillTarget -Recurse
```

### macOS / Linux

```bash
patent_skill_target="${CODEX_HOME:-$HOME/.codex}/skills/paper-to-patent-cn"
mkdir -p "$patent_skill_target"
cp SKILL.md "$patent_skill_target/"
cp -R references agents "$patent_skill_target/"
```

安装后按客户端的技能刷新方式加载，必要时重新打开会话。其他支持 `SKILL.md` 的客户端可以使用同一正文与参考文件，安装位置和调用语法以对应客户端为准。

## 使用示例

```text
请使用 $paper-to-patent-cn，根据附件论文和设计文档撰写中文发明专利申请稿，参考我提供的专利格式。
```

```text
请使用 $paper-to-patent-cn，仅精简这份稿件的权利要求，尽量控制在10项，不修改其他章节。
```

```text
请使用 $paper-to-patent-cn，根据这份 README 的技术方案修改实施例。未实现的设计按拟实施方案描述，不虚构实验效果。
```

## 写作与交付约定

采用中文标题，专业术语首次解释，以段落叙述为主。权利要求中的方法步骤不带 Sxxx 编号；公共步骤在实施例之前集中说明。核心方案、可选改进和实现示例分层表达，非必要参数不固化为基本方案限制。

完整稿的基础图为方法流程图和系统结构图；图1采用框旁曲线标注步骤，图2使用虚线框归组模块。其他图按需增加，涉及执行载体的实现图放在最后。摘要附图默认文字指定已有图号，不重复插图。这些均是可由明确用户要求覆盖的写作约定。

文件默认按“文档基础名_v版本号_修订核心点”保存，保留既有版本。仅要求文字时直接交付正文，不强制中间交底书、额外变更日志或其他工作流产物。

## 环境与可选能力

本仓库仅包含技能说明和参考文档，无需安装仓库专用脚本或运行时。联网检索需要客户端提供浏览或搜索能力；DOCX 生成与检查需要可用的文档工具。在 Codex 中可配合 `documents` 技能使用，仓库不捆绑该技能或其工具。

Word 的页面、字体、段落、公式、图片与分页约定集中在 `figures-and-docx.md`。用户模板优先，无模板时采用审阅稿默认值；正式提交按适用模板和提交要求核对。

## 贡献与许可

欢迎通过 Issue 或 Pull Request 改进通用表达、模块加载边界和文档兼容性。示例请使用合成或已获授权的内容，避免提交未公开论文、专利稿、凭据和私人路径。

本项目采用 [MIT License](LICENSE)。
