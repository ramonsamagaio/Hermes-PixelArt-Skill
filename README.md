# 🎨 Hermes Pixel Art Texturing Bible

> Complete pixel art texturing bible for low-poly 3D models, inspired by Valheim and Wickwild.

## What is it

A Hermes Agent skill containing everything an agent needs to texture low-poly 3D models with pixel art style: painting techniques, biomes palettes, UV→Engine workflow, procedural automation, and a complete从零tutorial.

## Installation

### Via Hermes CLI (recommended)

```bash
hermes skills install https://raw.githubusercontent.com/ramonsamagaio/Hermes-PixelArt-Skill/main/SKILL.md
```

### Manual

```bash
# Clone the repository
git clone https://github.com/ramonsamagaio/Hermes-PixelArt-Skill.git

# Copy to Hermes skills directory
cp -r Hermes-PixelArt-Skill ~/.hermes/skills/pixel-art-texturing-bible
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

### 1. Load the skill

In Hermes chat:

```
/skill pixel-art-texturing-bible
```

Or ask the agent: *"Load the pixel-art-texturing-bible skill"*

### 2. Follow the workflow

The skill guides you through:
1. **Preparation** — UV unwrap and template
2. **Painting** — techniques per material (wood, stone, dirt, foliage)
3. **Testing** — engine settings (Point filtering, no mipmaps)
4. **Polishing** — moss, wetness, wear in coherent regions

### 3. Use the palettes

Each Wickwild biome has defined palettes. Copy hex values from `references/palettes.md`.

### 4. Avoid anti-patterns

The 10 most common errors are documented with "good" vs "bad" pixel visual examples.

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

Every texture is rated 1-10 on:
- Legibility
- Consistency
- Aesthetics
- Technique
- Performance

**Goal: minimum 9/10 in each category.**

## Compatible Tools

- Aseprite (recommended)
- GIMP
- Krita
- Photoshop
- Procreate
- Pixilart (web)

## License

MIT

---

**Part of the Hermes Agent ecosystem.** See also: [Hermes-Pixelorama-MCP](https://github.com/ramonsamagaio/Hermes-Pixelorama-MCP) for direct Pixelorama integration.
