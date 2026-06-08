[中文](./README.zh-CN.md) | [English](./README.md)

# Skills

[![license](https://img.shields.io/badge/license-MIT-007EC6)](./LICENSE)

## What Is This

This is a collection of skills for doing AI coding better. It includes the skills I use regularly, both self-made and selected third-party open-source ones, and supports installation across platforms such as Codex and Claude Code.

## Philosophy and Goals

> AI coding should not be understood as only "AI writing code". It should be treated as the complete working loop of a real software engineer.

Since the rise of Vibe Coding, many people have had the illusion that saying a few words to an AI is enough to get a production-ready product. In my view, that "product" can only serve as an experimental MVP (Minimum Viable Product), or it ends up being a toy.

It may look like it works, but as iteration continues, many fatal issues can emerge and eventually bring it down, for example:

- Goal drift: insufficient requirement breakdown
- Software quality:
  - performance problems
  - architecture and code rot
- Loss of control: when problems happen, only the AI can participate, while the developer becomes a bystander

What really matters is that AI can speed up work across different stages, but it should not remove stages from the development process. To ensure software maturity, there should be at least the following steps, among others:

- Requirement analysis and planning: feature breakdown, technical architecture, and code design
- Coding and implementation: a good implementation should ensure usability, ease of use, readability, extensibility, and maintainability
- Software testing: verify whether behavior matches the requirements, and detect vulnerabilities, performance issues, and more
- Code review: inspect code quality and check whether the implementation is aligned with the requirements

Clearly, software development is not as simple as people imagine.

## Installation

The skills in this repository follow the standard `SKILL.md` structure and can be installed directly with [vercel-labs/skills](https://github.com/vercel-labs/skills):

```bash
npx skills add ShijayHuo/awesome-skills --list
npx skills add ShijayHuo/awesome-skills --skill <skill-name>
npx skills add ShijayHuo/awesome-skills --skill <skill-name> -a codex -g
```

## Skill List

### Essentials

- [/grill-with-docs](./skills/grill-with-docs/SKILL.md) - Align requirements, break down features, unify domain terms and concepts, and sync the results into `CONTEXT.md` and architecture decision records (ADRs). This skill comes entirely from [Mattpocock: Grill with doc](https://github.com/mattpocock/skills/blob/main/skills/engineering/grill-with-docs/SKILL.md).
- [/tdd](./skills/tdd/SKILL.md) - Test-driven development. This skill comes entirely from [Mattpocock: TDD](https://github.com/mattpocock/skills/blob/main/skills/engineering/tdd/SKILL.md).
- [/review](./skills/review/SKILL.md) - Code review to verify whether the implementation matches the feature requirements and whether the code follows standards such as naming, architecture layering, component conventions, and so on. This skill comes entirely from [Mattpocock: Review](https://github.com/mattpocock/skills/blob/main/skills/in-progress/review/SKILL.md).
- [/diagnose](./skills/diagnose/SKILL.md) - Bug fixing. Suitable for prompts such as "diagnose this" or "debug this", for reported defects, for cases where a feature is broken, throwing exceptions, or failing, and for performance regressions. This skill comes entirely from [Mattpocock: diagnose](https://github.com/mattpocock/skills/blob/main/skills/engineering/diagnose/SKILL.md).
- `/commit-and-push` - Commit and push a remote branch, create a draft pull request, and check or bind the related documentation and issues.
- [/clean-code](./skills/clean-code/SKILL.md) - Clean up code based on the principles of *Clean Code*. This skill comes entirely from this repository's local skill document, currently imported from [antigravity-awesome-skills @ 9d486d0](https://github.com/sickn33/antigravity-awesome-skills/blob/9d486d0899e0c4474939861469ac43339f128344/skills/clean-code/SKILL.md).

### Commonly Used, Personal Preference

- [/to-issues](./skills/to-issues/SKILL.md) - Break task plans, specs, or PRDs into independently actionable GitHub issues for lightweight task management. This skill comes entirely from [Mattpocock: To issues](https://github.com/mattpocock/skills/blob/main/skills/engineering/to-issues/SKILL.md).
- [/handoff](./skills/handoff/SKILL.md) - Compact the current conversation into a handoff document so another agent can continue from the right context. This skill comes entirely from [Mattpocock: Handoff](https://github.com/mattpocock/skills/blob/main/skills/productivity/handoff/SKILL.md).
- `/ddd` - Four-layer architecture practice for domain-driven design.
