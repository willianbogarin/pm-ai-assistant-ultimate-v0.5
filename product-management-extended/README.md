# Product Management Extended

A unified product management plugin that composes skills from two sources:

1. **Anthropic's product-management plugin** - Official knowledge-work-plugins marketplace
2. **Dean Peters' Product-Manager-Skills** - Comprehensive PM skills library

## Structure

```
product-management-extended/
├── .claude-plugin/
│   └── plugin.json          # Composes both skill directories
├── README.md                # This file
└── (symlinks to both sources)
```

## Skill Sources

### Anthropic's Product Management Skills
Located in: `../product-management/skills/`

Covers official Anthropic PM practices and tools.

### Dean Peters' Product Manager Skills
Located in: `../external/dean-peters/skills/`

Comprehensive library covering:
- Discovery & discovery processes
- Strategy frameworks (Ansoff, PESTEL, etc.)
- Market intelligence
- Customer journey mapping
- Competitive analysis
- Finance & metrics
- Career development
- And many more...

## Updating Skills

To pull the latest updates from Dean Peters' repo:

```bash
git submodule update --remote external/dean-peters
```

To update all submodules:

```bash
git submodule update --remote
```

## Usage

This plugin is designed to be installed locally in Claude Code. All available skills from both sources will be accessible when this plugin is enabled.

## Skills Count

- Anthropic product-management: ~X skills
- Dean Peters Product-Manager-Skills: ~85+ skills
- **Total: 85+ unified PM skills**
