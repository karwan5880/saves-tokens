# Compact command design

## Method

Ask tools for evidence and decisions, not raw noise: targeted `rg`, line ranges, one focused test, `git diff --stat` before full diffs, no ANSI/progress, and bounded logs.

## Preserve

Keep exit status, filenames, failing assertion, stack frames, error text, and exact patch/diff anchors. Re-run uncompressed when troubleshooting; stripping the diagnostic detail causes expensive retries.
