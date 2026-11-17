# Question Bank — Computer Vision · [OXFORD]
<!-- Appended by tutor sessions. Sprint: overlap decks only (02, 06, 07, 08, 09, 16, 17, 18); full course in phase 2. -->

> ⚠️ **EMPTY as of 2026-11-11 (D56) — flagged, not forgotten.** 20 CV decks are cached in `study/cache/cv/`; **zero questions are banked here.** The campaign is scheduled to turn CV-only on **20 Nov** and the assessment is **25 Dec (T-44)**, so this is not yet late — but it is the one genuinely hollow artefact on the board, and it was found by an audit that initially *passed* it, because the file exists. Mining starts 20 Nov per SYLLABUS Block 5; the eight overlap decks (02, 06, 07, 08, 09, 16, 17, 18) are the first targets since they were taught in Blocks 1–2 and are half-warm. Recorded here so that the first CV window does not arrive expecting a bank that was never written.

---

## Mined 2026-11-17 (D62) — overlap decks, batch 1

*The pause on **serving** CV holds until 20 Nov; mining the bank is not serving. Built now so the first CV window has something to draw on rather than arriving empty — the same mistake as the mock that was discussed for nine Saturdays and never written. No arithmetic in any item: both completed orals were structural, and the CV assessment is assumed the same until told otherwise.*

### QB-CV-0001 · [OXFORD] · forced-choice direction · `02_Filtering` — "Nyquist-Shannon sampling theorem" · not yet asked
The theorem says the sampling frequency must be **at least twice** the maximum frequency in the signal to reconstruct it perfectly.
**(a)** You halve the sampling rate on a detailed texture. Does the problem come from frequencies *above* or *below* the new limit?
**(b)** Name what you see when it goes wrong — the deck gives three symptoms.
> Above. Content above half the sampling rate cannot be represented and **masquerades as low-frequency content** — that impersonation is what "aliasing" names. Deck's symptoms: **disintegrating textures, Moiré patterns, false colour.**

### QB-CV-0002 · [OXFORD] · mechanism, "why deliberately destroy information" · `02_Filtering` — "Anti-aliasing" · not yet asked
The deck's fix: *before* sampling, remove all frequencies greater than half the new sampling frequency — and it says plainly this **loses information, but is still better than aliasing.**
**Why is throwing information away the better option?** Answer as a mechanism, not "because aliasing is bad."
> Because the high frequencies are not merely lost when you subsample — they are **re-encoded as false low frequencies** that are indistinguishable from real signal, so they corrupt the data you kept. Blurring first **deletes** them; subsampling without it **disguises** them. A known absence beats an unrecognisable lie.

### QB-CV-0003 · [OXFORD] · forced choice · `02_Filtering` — "Sampling and reconstruction" / "Images as Functions" · not yet asked
The deck frames an image two ways: as a grid of pixels, and as a **function**.
Which framing do you need to state the sampling theorem at all, and why can't the other one express it?
> The function view. Sampling theory is about **frequency content**, which only exists for a continuous signal being measured at intervals; a finished pixel grid is already the *result* of sampling and has no notion of what was lost. You cannot talk about exceeding a limit from inside the thing the limit produced.

### QB-CV-0004 · [OXFORD] · mechanism + the limit case · `07_CNNs` — "Parameter sharing" · not yet asked
The deck's justification: *"detecting e.g. an edge is important at any position of the image."*
**(a)** What property of images does that sentence assert?
**(b)** Name a vision task where the assertion is false.
> **(a)** Translation invariance of *what is worth detecting* — feature usefulness does not depend on location, so one filter can serve every position and every position becomes a training example for it. **(b)** It fails where position carries meaning: registered medical images with fixed anatomy, document layout, or anything where "top-left" is semantically different from "bottom-right". *(Same shape as the DL4H weight-sharing anchor — one fact, two courses.)*

### QB-CV-0005 · [OXFORD] · forced-choice direction · `07_CNNs` — "CNN Architecture" (stride) · not yet asked
The deck: **stride > 1 results in spatial sub-sampling of the feature maps.**
**(a)** Raise the stride — does the feature map get bigger or smaller, and what happens to the receptive field of the next layer measured in input pixels?
**(b)** Connect this to `QB-CV-0001`. What have you just done to the sampling rate, and what does the theorem then warn you about?
> **(a)** Smaller map; the next layer's receptive field grows, because each of its units now spans more input. **(b)** You have **subsampled** — so the theorem applies, and striding without blurring first is exactly the aliasing case. **This is the through-line worth having: stride is subsampling, and subsampling without a low-pass is aliasing.**

### QB-CV-0006 · [OXFORD] · structural, "which invariance" · `07_CNNs` — "Pooling Layers" / "Max-Pooling Example" · not yet asked
Max-pooling, 2×2 window, stride 2 — the deck's common case.
**(a)** What does it keep and what does it discard?
**(b)** What invariance does that buy, and state the cost in the same breath.
> **(a)** Keeps the **maximum response** in each window; discards *where in the window* it occurred and the other three values. **(b)** Buys **small-translation invariance** — the answer is unchanged if the feature shifts within the window — at the cost of **spatial precision**, which is why segmentation and localisation architectures either pool less or must recover the lost resolution later.
