# ppt-analyzer

A small command-line tool that analyzes PowerPoint (`.pptx`) files and reports
content stats and quality problems, so you can fix a deck before presenting it.

## What it checks

**Per slide:** title, word count, images, charts, tables, speaker-note length, smallest
font size.

**Warnings:** missing slide titles, text-heavy slides, tiny fonts, images without alt text.

**Deck-wide:** duplicate titles, too many fonts, no speaker notes, readability
(Flesch reading ease), estimated speaking time (~130 words/min), and an overall
quality score out of 100.

## Install

```bash
git clone https://github.com/<your-username>/ppt-analyzer.git
cd ppt-analyzer
pip install .
```

Or run without installing: `pip install -r requirements.txt` then `python -m ppt_analyzer ...`

## Usage

```bash
ppt-analyzer deck.pptx                         # readable text report
ppt-analyzer deck.pptx -f markdown -o report.md
ppt-analyzer deck.pptx -f json                 # machine-readable
ppt-analyzer ./presentations                   # every .pptx in a folder
ppt-analyzer deck.pptx --max-words 80 --min-font 14
ppt-analyzer deck.pptx --fail-under 70         # exit code 1 if score < 70 (good for CI)
```

Options: `-f/--format {text,json,markdown}`, `-o/--output`, `--max-words`, `--min-font`,
`--fail-under`.

## Use as a library

```python
from ppt_analyzer import analyze_file

report = analyze_file("deck.pptx")
print(report.score, report.est_minutes)
for slide in report.slides:
    for issue in slide.issues:
        print(slide.number, issue.message)
```

## Notes and limits

- Font sizes are only checked when set explicitly on the text; sizes inherited from
  the theme or layout are not resolved.
- Only `.pptx` is supported (not legacy `.ppt`; save it as `.pptx` first).
- The score is a simple heuristic, not a standard.

## Tests

```bash
pip install -e .[dev]
pytest
```

## License

MIT
