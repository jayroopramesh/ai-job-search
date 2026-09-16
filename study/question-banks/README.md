# Question Banks

One file per course. Questions are generated **just-in-time** from the Drive decks during sessions (TUTOR.md §1), then archived here so they are never re-asked verbatim and so mocks can sample from history.

Entry format (append-only, one block per item):

```md
### QB-DL4H-0001 · [OXFORD] · cloze · L2 p.12 · first asked 2026-09-18
Q: Training a neural network minimises ______ over the training data; the gap to true risk is controlled by ______.
A: empirical risk; generalisation (bounded via regularisation/validation)
Asked: 2026-09-18 ❌ · 2026-09-19 ✅ · 2026-09-22 ✅
Linked flag: FP-3 (cleared 2026-09-24)
```

Rules:
- ID = `QB-<COURSE>-<seq>`; never delete, mark `retired` if a deck changes.
- Format is one of the 11 in TUTOR.md §3; `Asked:` line tracks the testing history.
- Same concept re-attacked = NEW entry with different format/phrasing, cross-linked to the flag point.
