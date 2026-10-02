---
name: format-list
description: 'Convert CSV files or plain comma-separated lists into readable Markdown tables. Use when asked to format, tabulate, or make comma-separated data easier to read.'
argument-hint: '[path to a CSV or comma-separated list file]'
---

# Format List

Turn a comma-separated data file into a readable Markdown table without changing or discarding its contents.

## Procedure

1. Identify the input file from the user's path, selection, or currently open file. If none is clear, ask which file to format.
2. Inspect a small portion of the file to determine whether it is a structured CSV table with a header row or a plain list of comma-separated values. Check for quoted fields, embedded commas, blank lines, and a likely delimiter before parsing.
3. Parse CSV as CSV; never split each line directly on commas, since quoted values can contain commas or line breaks. Preserve the original field text and row order. Do not normalize, infer, or silently remove data.
4. For a headered CSV, use the first row as the table headings. If there is no header, use neutral headings such as `Column 1`, `Column 2` rather than inventing meanings. For a plain list, format each item as a row in a single-column table; trim only separator-adjacent whitespace.
5. Escape Markdown table syntax in values, especially `|`, and represent embedded line breaks so each record stays on one table row. Keep empty fields visibly empty.
6. Write the result as a sibling Markdown file with the same base name and a `.md` extension. Never overwrite or delete the source. If that output already exists, choose a non-conflicting filename or ask before replacing it.
7. For a large file, write the complete table to the output file instead of truncating it in chat. Report the output path and any parsing assumptions. If the source is malformed or its structure cannot be determined reliably, ask a focused question before producing a table.

## Completion Check

- The output contains one table row per input record or list item, excluding a header row when one exists.
- The table has the same number of columns for every row, and values containing commas remain intact.
- The original file is unchanged, and any assumptions or irregularities are reported.