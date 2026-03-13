# 5ymb01 Ticker -- Of The Day

> Part of [5ymb01 Ticker](https://github.com/5ymb01/5ymb01-ticker) | Based on [ChuckBuilds/ledmatrix-of-the-day](https://github.com/ChuckBuilds/ledmatrix-of-the-day)

## Custom Modifications

- **CodeRabbit compliance**: Category ID regex validation before file writes to prevent path traversal; narrowed bare exception handlers to specific types
- **Dead code removal**: Removed unused `_draw_bdf_text` method
- **Schema improvements**: Added `live_priority` field and `min_ledmatrix_version` to manifest for proper store compatibility

## Features

- **Multiple Categories**: Word of the Day, Bible verses, Slovenian words, or any custom daily content
- **Automatic Daily Updates**: Checks for new content each day (configurable interval)
- **Rotating Display**: Alternates between title/word view and definition/content view
- **Multi-line Text Wrapping**: Handles long definitions across multiple display lines
- **Self-contained Data**: All JSON data files stored within the plugin directory
- **Category Rotation**: Cycles through enabled categories on a timer
- **Web UI Config**: Full configuration through the LEDMatrix web interface, including a file manager widget for uploading/managing data files

## Configuration

Key settings in `config/config.json` under `of-the-day`:

| Setting | Default | Description |
|---------|---------|-------------|
| `enabled` | `false` | Enable the plugin |
| `update_interval` | `3600` | Seconds between checking for new day |
| `display_rotate_interval` | `20` | Seconds between category rotations |
| `subtitle_rotate_interval` | `10` | Seconds between title/content toggle |
| `display_duration` | `40` | Total display duration per cycle (seconds) |
| `category_order` | `["word_of_the_day",...]` | Display order of categories |
| `categories.<id>.enabled` | `true` | Enable/disable individual categories |
| `categories.<id>.data_file` | -- | Path to JSON file (relative to plugin dir) |
| `categories.<id>.display_name` | -- | Label shown in UI and on display |

### Data File Format

Each category uses a JSON file with date-keyed entries (`YYYY-MM-DD`):

```json
{
  "2025-10-11": {
    "word": "Ephemeral",
    "pronunciation": "ih-FEM-er-uhl",
    "type": "adjective",
    "definition": "Lasting for a very short time; transitory"
  }
}
```

Custom categories can use `word`/`title` for the heading and `definition`/`content`/`text` for the body.

### Adding a Category

1. Create a JSON data file in the plugin's `of_the_day/` directory
2. Add the category to `categories` in config with `enabled`, `data_file`, and `display_name`
3. Add the category ID to `category_order`

---
*Credits: [ChuckBuilds](https://github.com/ChuckBuilds) (original), [Claude Code](https://claude.ai/claude-code) (AI-assisted development)*
