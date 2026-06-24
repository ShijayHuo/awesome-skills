[中文](./README.zh-CN.md) | [English](./README.md)

# Skills

[![license](https://img.shields.io/badge/license-MIT-007EC6)](./LICENSE)

## 这是什么

这是一个用来更好 AI Coding 的 skills 收藏夹，收录了我常用的 skills（包含有自制和第三方开源的），支持安装到 Codex、Claude code 多个平台。

## 理念与目标

> AI Coding 不应该只理解为 AI 去编码这一件事，而更应该当做是一个真正的开发工程师的工作闭环。

自从 Vibe Coding 的出现让很多人都产生过错觉，认为只需要对着 AI 说几句话就能给你一个生产级的产品，于我而言，该“产品”只能作为实验性的 MVP（Minimum Viable Product）或者沦为“玩具”。它看起来能运转，但随着迭代，有产生很多致命的因素而导致落幕，比如：
- 目标偏离：需求拆解不足
- 软件质量：
  - 性能问题
  - 架构和代码的腐烂
- 失去控制权：出了问题，只有 AI 能参与，开发者成为旁观者

真正要说的是 AI 加快了各个环节生产速度，但不应该减少开发工作的环节，为保证软件的成熟度至少应该有（但不仅限于）：
- 需求分析和规划：功能拆解、技术架构和代码设计
- 编码开发：好的实现应该保证可用性、易用性、可读性、扩展性、可维护性等
- 软件测试：检测功能是否对齐、漏洞、性能问题等
- Code review：检查代码质量、审视代码实现是否与需求对齐

显然，软件开发这并非想象的那么简单。

## 安装

仓库里的 skill 采用标准 `SKILL.md` 结构，直接用[vercel-labs/skills](https://github.com/vercel-labs/skills)安装：

```bash
npx skills add ShijayHuo/awesome-skills --list
npx skills add ShijayHuo/awesome-skills --skill <skill-name>
npx skills add ShijayHuo/awesome-skills --skill <skill-name> -a codex -g
```
## skills 列表
### 必备
- [/key-decision-vetting](./skills/key-decision-vetting/SKILL.md) —— 一个有限且高信号的设计决策审查，聚焦最关键的分支与分歧，统一领域术语，并将结果同步到 CONTEXT.md 和架构决策记录（ADRs）。该 skill 基于 [Mattpocock: Grill with doc](https://github.com/mattpocock/skills/blob/main/skills/engineering/grill-with-docs/SKILL.md) 优化。
- [/code-implement](./skills/code-implement/SKILL.md) —— 在新增功能、修改现有代码或重构实现时，结合项目的 CONTEXT.md 和相关 ADRs 评估复杂度与风险，并选择合适的改动方案。该 skill 当前以本仓库内的本地文档为准，并参考了 [antigravity-awesome-skills](https://github.com/sickn33/antigravity-awesome-skills/blob/main/skills/clean-code/SKILL.md) 和 [Mattpocock: TDD](https://github.com/mattpocock/skills/blob/main/skills/engineering/tdd/SKILL.md)。
- [/review](./skills/review/SKILL.md) —— 代码审查，验证实现是否与功能对齐、代码是否符合规范，如命名、架构分层、组件规范等等。该 skill 完全来源于 [Mattpocock: Review](https://github.com/mattpocock/skills/blob/main/skills/in-progress/review/SKILL.md)
- [/diagnose](./skills/diagnose/SKILL.md) —— 修复漏洞，适用于提出“诊断此问题”/“调试此问题”、报告缺陷、指出某些功能出现故障/抛出异常/失败，或描述性能退化的情况。该 skill 完全来源于 [Mattpocock: diagnose](https://github.com/mattpocock/skills/blob/main/skills/engineering/diagnose/SKILL.md)。

### 常用，个人偏好
- [/to-issues](./skills/to-issues/SKILL.md) —— 将任务计划、规范或 PRD 分解为可独立获取的 GitHub 问题，适用于做轻量任务管理。该 skill 完全来源于 [Mattpocock: To issues](https://github.com/mattpocock/skills/blob/main/skills/engineering/to-issues/SKILL.md)
- [/handoff](./skills/handoff/SKILL.md) —— 将当前对话压缩成一个可交接文档，方便下一位 agent 直接接手。该 skill 完全来源于 [Mattpocock: Handoff](https://github.com/mattpocock/skills/blob/main/skills/productivity/handoff/SKILL.md)。
- `/ddd` —— 领域驱动设计四层架构实践
