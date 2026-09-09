# 安装与更新指南

## 前置条件

- 已安装支持本地 Skills 的 Codex 或兼容智能体。
- 本机可以使用 Git；也可以从 GitHub 下载 ZIP 后手动安装。

## Windows PowerShell 安装

```powershell
git clone https://github.com/liyue-aigc/female-outfit-director.git
New-Item -ItemType Directory -Force "$HOME\.codex\skills\female-outfit-director"
Copy-Item -Recurse -Force ".\female-outfit-director\skill\*" "$HOME\.codex\skills\female-outfit-director\"
```

安装后的关键文件应位于：

```text
%USERPROFILE%\.codex\skills\female-outfit-director\SKILL.md
%USERPROFILE%\.codex\skills\female-outfit-director\agents\openai.yaml
%USERPROFILE%\.codex\skills\female-outfit-director\references\output-contract.md
%USERPROFILE%\.codex\skills\female-outfit-director\references\parameter-presets.md
%USERPROFILE%\.codex\skills\female-outfit-director\references\transition-library.md
```

## macOS / Linux 安装

```bash
git clone https://github.com/liyue-aigc/female-outfit-director.git
mkdir -p ~/.codex/skills/female-outfit-director
cp -R female-outfit-director/skill/. ~/.codex/skills/female-outfit-director/
```

## 下载 ZIP 安装

1. 在仓库页面选择 **Code → Download ZIP**。
2. 解压下载文件。
3. 找到解压目录中的 `skill` 文件夹。
4. 将 `skill` 内部的全部内容复制到：
   - Windows：`C:\Users\你的用户名\.codex\skills\female-outfit-director\`
   - macOS / Linux：`~/.codex/skills/female-outfit-director/`
5. 确保 `SKILL.md` 直接位于 `female-outfit-director` 目录下，而不是额外嵌套在 `skill` 子目录中。

## 验证安装

重新打开 Codex 任务，然后输入：

```text
$female-outfit-director 请先介绍你能生成哪些类型的女性换装方案。
```

如果 Skill 被正确识别，它会依据工作流说明换装模式、参数和输出结构。

## 更新

在已克隆的仓库目录中执行：

```powershell
git pull
Copy-Item -Recurse -Force ".\skill\*" "$HOME\.codex\skills\female-outfit-director\"
```

macOS / Linux：

```bash
git pull
cp -R skill/. ~/.codex/skills/female-outfit-director/
```

更新后新建一个 Codex 任务，以确保加载最新的 Skill 内容。

## 卸载

确认目录无自定义修改后，删除本地 Skill 目录即可：

```powershell
Remove-Item -Recurse "$HOME\.codex\skills\female-outfit-director"
```

卸载只影响本地 Skill，不会删除你已经生成的提示词、图片或视频。
