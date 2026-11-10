# Help: using ppt-analyzer and uploading it to GitHub

## 1. Run the tool on your computer

1. Install Python 3.9 or newer from python.org (tick "Add Python to PATH" on Windows).
2. Open a terminal in the `ppt-analyzer` folder and install it:
   ```bash
   pip install .
   ```
3. Analyze a presentation:
   ```bash
   ppt-analyzer my-deck.pptx
   ```
   If the `ppt-analyzer` command isn't found, use `python -m ppt_analyzer my-deck.pptx` instead.

### Reading the report
| Line | Meaning |
|---|---|
| Est. speaking time | Words divided by about 130 words per minute (speaker notes are used when present) |
| Reading ease | Flesch score: 60+ is easy, below 30 is hard |
| Quality score | 100 minus penalties for warnings and deck issues |
| `[warning]` | Worth fixing: missing title, too many words, tiny font, image without alt text |
| `[info]` | Suggestion: duplicate titles, many fonts, no speaker notes |

### Useful options
| Option | What it does |
|---|---|
| `-f markdown -o report.md` | Save the report as a Markdown file |
| `-f json` | Output JSON for other programs |
| `--max-words 80` | Warn when a slide has more than 80 words |
| `--min-font 14` | Warn about fonts smaller than 14 pt |
| `--fail-under 70` | Exit with an error if the score is below 70 |

## 2. Upload to GitHub (no command line)

1. Unzip `ppt-analyzer.zip`.
2. Sign in at github.com, click **+** (top right), then **New repository**.
3. Name it `ppt-analyzer`, leave it Public, and click **Create repository**.
4. Click **uploading an existing file**.
5. Open the unzipped folder and drag in **everything inside it**: the `ppt_analyzer` folder, `tests`, `README.md`, `HELP.md`, `LICENSE`, `pyproject.toml`, `requirements.txt` and `.gitignore`. Dragging the folders keeps their structure.
6. Click **Commit changes**.

## 3. Upload to GitHub (command line)

First create an empty repository on github.com, then run in the project folder:
```bash
git init
git add .
git commit -m "Initial commit"
git branch -M main
git remote add origin https://github.com/<your-username>/ppt-analyzer.git
git push -u origin main
```

## 4. Before you publish

- Open `LICENSE` and replace `<your name>` with your name.
- Open `README.md` and replace `<your-username>` with your GitHub username.

## 5. Troubleshooting

| Problem | Fix |
|---|---|
| `Could not read ... file is not a zip file` | The file isn't a real `.pptx`. Open it in PowerPoint and Save As `.pptx`. |
| Old `.ppt` file | Not supported. Save it as `.pptx` first. |
| `No .pptx files found` | Check the path, or pass a folder that contains `.pptx` files. |
| `pip` not found | Try `python -m pip install .` |
| Files starting with `~$` are skipped | Those are temporary lock files PowerPoint creates while a deck is open. |
