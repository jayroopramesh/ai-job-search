# Deck text cache

Extracted 2026-09-16 via Drive `read_file_content` so tutoring runs cache-first (TUTOR.md §1) and works even when a wake has no Drive tools. `[Page N]` markers give slide numbers for citations.

Known limitations:
- **Math glyphs are mangled** by text extraction — always verify a formula visually in the source PDF (RESOURCES.md has file IDs) before quizzing it.
- **Tail truncation**: Drive's extraction can cut off the last slides of large decks. Observed in introml 01, 07, 08, 09, 13, 15 (end mid-sentence). When covering late-deck topics, cross-check the PDF tail visually and append missing content to the cache file.
- Figures are not captured — picture questions always go back to the PDF (pymupdf raster).

Refresh policy: when the daily sync (§7) sees a changed/new Drive file, re-extract and overwrite/add the cache file in the same commit that updates RESOURCES.md.
