# Claude Skills Hub

Claude Code 技能 Skill 集合，提供专业领域的分析框架和方法论。

## 技能列表

| 技能名称            | 描述      | 使用场景           | 文档                                           |
| --------------- | ------- | -------------- | -------------------------------------------- |
| 局观（game-theory） | 博弈论决策分析 | 商业博弈、人际博弈、股市博弈 | [技能文档](game-theory.md)、 [案例文档](doc/game-theory-output/贵州茅台博弈分析报告.md) |

## 目录结构

```
skill_hub/
├── skills/                    # 技能源码
│   └── game-theory/          # 博弈论技能
│       ├── SKILL.md          # 技能主文件
│       └── references/       # 参考文档
├── doc/                       # 技能文档与输出示例
│   └── game-theory-output/   # 博弈论分析报告示例
└── README.md
```

## 安装技能

### 一键安装

#### 局观（game-theory）

```bash
npx skills add Shkin1/skill-hub --skill game-theory -a claude-code -g -y
```

## 使用方法

安装后，在 Claude Code 中直接提问，技能会根据关键词自动触发。

## 开发新技能

```
skills/
└── your-skill/
    ├── SKILL.md              # 技能主文件（必需）
    └── references/           # 参考文档（可选）
```

SKILL.md 格式：

```markdown
---
name: skill-name
description: 技能描述
---

# 技能内容
...
```

## License

MIT License
