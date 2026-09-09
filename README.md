# 女性换装导演

`female-outfit-director` 是一个面向 Codex / Skills 兼容智能体的中文工作流 Skill，用来生成“同一位成年女性、多套穿搭拼贴首帧、卡点换装视频”的完整制作方案。

它会把人物设定、服装方案、拼贴布局、换装机制、动作连续性和声音节点整理为可直接用于图像与视频生成模型的结构化提示词。

## 主要能力

- 根据参考图锁定人物五官、发型、气质与身份一致性。
- 没有参考图且未指定国籍时，默认使用原创中国成年女性角色。
- 生成同一角色的五套穿搭拼贴首帧提示词。
- 输出逐段视频时间轴、精简视频提示词和负面约束。
- 使用固定输出契约检查五项交付是否齐全、时间段是否连续、图片位置与视频触发方向是否对应。
- 内置 12 种换装机制，覆盖人物贴图飞入、衣袖遮镜、旋身接力、贴纸翻页、动作卡点等方案。
- 支持用户锁定时长、比例、镜头、服装、卡点时间、音乐和动作。

## 当前默认规则

- 画幅：9:16。
- 时长：8 秒。
- 造型数量：5 套，包括初始造型和 4 次换装。
- 构图：中央大人物，加四个悬浮完整人物贴图。
- 镜头：固定机位。
- 声音：默认无背景音乐，仅保留换装所需的点击、飞入和卡点音效；用户指定音乐时按要求编排。
- 输出：参数锁定结果、首帧图片提示词、逐段视频时间轴、精简视频提示词、负面提示词。

用户明确给出的参数始终优先于默认值，因此也可以要求 15 秒舞蹈、不同人物数量、其它镜头或自定义卡点。

## M1 消耗式贴图换装

默认的 M1 机制采用“复制飞入、原位消耗”规则：

1. 点击目标小人物贴图。
2. 复制出一个完整人物抠像作为飞入副本。
3. 原位置的小人物立即移除，原位置留空。
4. 飞入副本向中央移动并快速放大。
5. 副本与中央人物的头、肩、腰及动作姿态对齐，触发换装。
6. 飞入副本和白色虚线轮廓同时消失，中央只保留一个换装后人物。

换装完成后不会保留已经使用的小人物贴图，也不会产生中央人物重影。

## 快速安装

完整步骤见 [安装与更新指南](docs/INSTALLATION.md)。

```powershell
git clone https://github.com/liyue-aigc/female-outfit-director.git
New-Item -ItemType Directory -Force "$HOME\.codex\skills\female-outfit-director"
Copy-Item -Recurse -Force ".\female-outfit-director\skill\*" "$HOME\.codex\skills\female-outfit-director\"
```

安装后重新打开 Codex 任务，并使用：

```text
$female-outfit-director 帮我为同一位中国成年女性设计五套都市穿搭拼贴首帧，并生成8秒卡点换装视频脚本。
```

第一次使用建议阅读 [首次使用教程](docs/FIRST_USE.md)。

## 仓库结构

```text
female-outfit-director/
├─ skill/                         # 可直接安装的 Skill
│  ├─ SKILL.md
│  ├─ agents/openai.yaml
│  └─ references/
│     ├─ output-contract.md
│     ├─ parameter-presets.md
│     └─ transition-library.md
├─ docs/
│  ├─ INSTALLATION.md
│  └─ FIRST_USE.md
├─ CHANGELOG.md
├─ CONTRIBUTING.md
├─ LICENSE
└─ README.md
```

## 兼容性

- 支持本地 Skills 的 Codex 或兼容智能体。
- 使用参考图时，建议使用具备图像理解能力的模型。
- 本仓库只提供提示词导演工作流，不包含第三方图像或视频生成服务。

## 参与贡献

问题反馈和改进建议请参考 [CONTRIBUTING.md](CONTRIBUTING.md)。

## License

[MIT License](LICENSE) © 2026 liyue-aigc
