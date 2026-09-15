# 🎨 Pixel Art Texturing Bible

> Complete pixel art texturing bible for low-poly 3D models, inspired by Valheim and Wickwild. Works with any AI agent.

![Pixel Art Texturing](https://github.com/user-attachments/assets/92307956-5e15-4575-9da8-5014e164083b)

## What is it

A comprehensive skill containing everything an AI agent needs to texture low-poly 3D models with pixel art style: painting techniques, biomes palettes, UV→Engine workflow, procedural automation, and a complete step-by-step tutorial.

## Compatible Agents

Works with any AI agent that supports skills or markdown context:

- **Hermes Agent** — `hermes skills install` or `/skill pixel-art-texturing-bible`
- **Claude Code / Claude Desktop** — paste SKILL.md into context or use as reference
- **ChatGPT / GPT** — paste into custom instructions or project context
- **Cursor, Windsurf, Cline, Continue, Aider, Codex** — load as project context or reference
- **Any agent** — the markdown files are universally readable

## Installation

### Via Hermes CLI (recommended)

```bash
hermes skills install https://raw.githubusercontent.com/ramonsamagaio/Hermes-PixelArt-Skill/main/SKILL.md
```

### Manual (any agent)

```bash
git clone https://github.com/ramonsamagaio/Hermes-PixelArt-Skill.git

# Hermes: copy to skills directory
cp -r Hermes-PixelArt-Skill ~/.hermes/skills/pixel-art-texturing-bible

# Claude/GPT/Cursor: paste SKILL.md into your project context or .cursorrules
# Aider: reference the files in your project directory
```

### For Claude Code

Add to your project's `CLAUDE.md`:

```markdown
# Pixel Art Texturing Rules
When texturing low-poly 3D models, follow the pixel art texturing bible:
- Read SKILL.md for complete workflow
- Use references/techniques.md for material-specific painting
- Use references/palettes.md for biome color palettes
- Use references/workflow.md for UV-to-engine pipeline
```

### For ChatGPT / GPT

Paste the SKILL.md content into your custom instructions. The agent will follow the workflow when asked to texture 3D models.

### For Cursor / Windsurf / Cline

Add to `.cursorrules`, `.windsurf/rules.md`, or `.cline/rules`:

```markdown
# Pixel Art Texturing
When working on 3D model texturing, use the pixel art texturing bible in this project.
Read SKILL.md for the complete workflow before starting any texture work.
```

## Structure

```
pixel-art-texturing-bible/
├── SKILL.md                          # Main bible (read first)
└── references/
    ├── techniques.md                 # Painting techniques per material
    ├── workflow.md                   # Complete model-to-engine workflow
    ├── examples.md                   # Visual ASCII art examples
    ├── anti-patterns.md              # 10 common errors and how to fix them
    ├── procedural.md                 # Python/Aseprite script automation
    ├── palettes.md                   # Hex palettes per biome (Deepwood, Fen, etc.)
    ├── first-asset-tutorial.md       # Complete tutorial: barrel from scratch to engine
    └── quick-reference.md            # Quick reference card (1 page)
```

## How to Use

**Hermes:**
```
/skill pixel-art-texturing-bible
```

**Claude/GPT/Cursor:** Paste SKILL.md into context or reference it in your prompt.

**Any agent:** "Use the pixel art texturing bible in this project to texture this model."

### Workflow

1. **Preparation** — UV unwrap and template
2. **Painting** — techniques per material (wood, stone, dirt, foliage)
3. **Testing** — engine settings (Point filtering, no mipmaps)
4. **Polishing** — moss, wetness, wear in coherent regions

## Key Principles

| Principle | Description |
|-----------|-------------|
| **Big blocks** | No photographic micro-noise |
| **Restricted palette** | 4-8 colors per material |
| **Hard transitions** | No smooth gradients |
| **Point filtering** | Sharp texture in engine |
| **Each pixel with purpose** | No isolated noise |

## Target Visual Style

- **Valheim** — main reference: hand-painted, big blocks, earthy colors
- **Wickwild** — stylized variation: biome palettes, dense atmosphere, procedural
- **Don't Starve / Northgard** — stylized with clear form

## Quality Checklist

Every texture is rated 1-10 on: Legibility, Consistency, Aesthetics, Technique, Performance.

**Goal: minimum 9/10 in each category.**

## Compatible Tools

- Aseprite (recommended), GIMP, Krita, Photoshop, Procreate, Pixilart (web)

## License

MIT

---

**Part of the pixel art ecosystem.** See also: [Pixelorama-MCP](https://github.com/ramonsamagaio/Hermes-Pixelorama-MCP) for direct Pixelorama integration from any AI agent.
