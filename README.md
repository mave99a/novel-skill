# Novel Creator Skill

Transform story ideas into complete novels with EPUB output through an interactive RPG-style workflow.

## Features

- **Interactive Story Building**: Guide users through key plot decisions using an RPG-style choice system
- **Structured Writing Process**: 5-phase workflow from concept to finished ebook
- **Professional EPUB Generation**: Auto-converts markdown chapters to beautifully formatted ebooks
- **Chinese Novel Optimization**: Built-in support for Chinese typography, poetry pairings, and literary styles
- **Customizable Writing Styles**: Support for various genres and literary influences (e.g., 琼瑶, 张爱玲)

## Workflow Overview

```
[Story Concept] → [Interactive RPG] → [Writing Plan] → [Chapters] → [EPUB]
     Phase 1           Phase 2           Phase 3        Phase 4     Phase 5
```

### Phase 1: Story Setup
Gather core story elements through interactive questions:
- Genre (穿越/Fantasy/Romance/Mystery)
- Setting (Ancient palace/Modern city/Fantasy world)
- Protagonist details
- Story goals and length

### Phase 2: Interactive RPG
Run 10-15 decision points where the user makes meaningful choices:
- Present vivid scene descriptions
- Offer 3-4 choices via `AskUserQuestion`
- Track consequences and plot development
- Weave in romance, conflict, and character growth

### Phase 3: Writing Plan
Generate a comprehensive `task_plan.md` including:
- Character profiles and arcs
- Foreshadowing matrix
- Chapter-by-chapter outline
- Poetry/lyrics pairings (for Chinese novels)
- Progress tracking table

### Phase 4: Chapter Writing
Write each chapter (~4000-5500 words) with:
- Opening and closing song lyrics/poetry
- Vivid sensory descriptions
- Character internal monologue
- Proper pacing and chapter-end hooks
- Consistent file naming: `[##]_[章节标题].md`

### Phase 5: EPUB Generation
Auto-generate professional ebook with:
- Cover page with title/author
- Table of contents
- Chinese typography CSS
- Proper chapter formatting

## Installation

### Prerequisites
- Python 3.7+
- Claude Code CLI

### Install from Marketplace
```bash
# Add the marketplace
/plugin marketplace add mave99a/novel-skill

# Install the plugin
/plugin install novel-creator
```

### Manual Setup
```bash
# Install required Python package
pip install ebooklib

# Clone and add as local plugin
git clone https://github.com/mave99a/novel-skill.git
/plugin add ./novel-skill
```

## Usage

### Quick Commands

| User Request | Action |
|-------------|--------|
| `写一部小说` / `Write a novel` | Full workflow (Phase 1-5) |
| `根据大纲写小说` + outline | Start from Phase 3 |
| `把章节转成epub` | Phase 5 only |
| `继续写下一章` | Resume Phase 4 |

### Example Session

```
User: 写一部小说

Claude: [Asks about genre, setting, protagonist...]

User: [Makes choices]

Claude: [Runs interactive RPG scenes, user makes plot decisions]

Claude: [Creates writing plan, writes chapters, generates EPUB]

Output: novel_title.epub
```

### EPUB Generator CLI

```bash
python3 scripts/create_epub.py [options]

Options:
    --title TITLE       Book title (auto-detects from task_plan.md)
    --author AUTHOR     Author name (default: "Claude AI")
    --path PATH         Chapter directory (default: current)
    --output OUTPUT     Output filename (default: [title].epub)
    --subtitle SUBTITLE Book subtitle/tagline
```

## File Structure

```
novel-skill/
├── .claude-plugin/
│   ├── plugin.json        # Plugin manifest for Claude Code
│   └── marketplace.json   # Marketplace catalog
├── skills/
│   └── novel-creator/
│       ├── SKILL.md       # Skill definition
│       ├── scripts/
│       │   └── create_epub.py
│       └── references/
│           ├── personas.md
│           └── poetry_pairs.md
├── samples/               # Example novel outputs
├── README.md              # This file
├── LICENSE                # MIT License
├── CHANGELOG.md           # Version history
└── requirements.txt       # Python dependencies
```

## Output Structure

When a novel is created, the following files are generated:

```
your-project/
├── task_plan.md           # Writing plan with outlines
├── 01_章节标题.md          # Chapter 1
├── 02_章节标题.md          # Chapter 2
├── ...
├── 10_章节标题.md          # Chapter 10
└── 书名.epub              # Final EPUB ebook
```

## Writing Style Guidelines

The skill supports customizable writing styles:

### Supported Influences
- **琼瑶 (Chiung Yao)**: Romantic, emotional dialogues, dramatic conflicts
- **张爱玲 (Eileen Chang)**: Rich imagery, psychological depth, subtle emotions
- **金庸 (Jin Yong)**: Martial arts, chivalry, intricate plots
- **Custom**: Any style specified by user

### Key Writing Elements
- Long, flowing paragraphs (avoid excessive short sentences)
- Deep psychological descriptions
- Sensory-rich scene setting
- Romantic tension in ambiguous scenes
- Proper use of Chinese literary devices

## Customization

### Adding New Genres
Edit `skill.md` to add new genre options in Phase 1.

### Modifying Chapter Structure
The default structure includes:
- Opening lyrics/poetry quote
- 3 main scenes per chapter
- Closing lyrics/poetry quote
- Chapter-end hook

Modify `skill.md` Phase 4 section to customize.

### Styling EPUB Output
Edit `scripts/create_epub.py` function `get_css_style()` to customize:
- Fonts
- Line spacing
- Quote styling
- Chapter heading appearance

## Examples

### Generated Novel Sample
- **Title**: 《误入心扉》
- **Genre**: Modern Urban Romance
- **Length**: 10 chapters, ~50,000 words
- **Features**: Office romance, family revenge, identity mystery, dramatic twists

### Chapter Naming Convention
```
01_当女孩遇见男孩.md
02_月光下的三明治.md
03_流言蜚语飞满天.md
...
```

## Troubleshooting

### EPUB Generation Fails
```bash
# Ensure ebooklib is installed
pip install ebooklib

# Check chapter file naming (must match patterns):
# - XX_title.md (e.g., 01_chapter.md)
# - 第X章_title.md
# - chapter_X.md
```

### No Chapters Found
Ensure your markdown files follow the naming convention and are in the correct directory.

### Chinese Characters Display Issues
The EPUB uses fallback fonts. Ensure your ebook reader supports Chinese fonts:
- Songti SC
- SimSun
- Noto Serif CJK SC

## Contributing

Contributions are welcome! Areas for improvement:
- Additional genre templates
- More reference materials (personas, poetry)
- Enhanced EPUB styling
- Multi-language support
- Cover image generation

## License

MIT License - Feel free to use and modify for your projects.

## Credits

- Created with Claude Code
- EPUB generation powered by [ebooklib](https://github.com/aerkalov/ebooklib)
