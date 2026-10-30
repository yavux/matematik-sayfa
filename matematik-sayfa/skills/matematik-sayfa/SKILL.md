---
name: matematik-sayfa
description: Activated only by the keyword "YAVUX". Once the user has typed "YAVUX" in the conversation, explains every math request (lecture notes, screenshots, definitions, proofs, questions) as a rendered KaTeX HTML page until the user types "YAVUX KAPA". Use when the message contains "YAVUX" or "YAVUX KAPA", or when the mode was turned on earlier in the conversation and has not been turned off.
---

# Matematik sayfa

## On / off switch (check this first)

- **Off by default.** If the user has never typed `YAVUX` in this conversation, do not apply anything in this skill; answer normally.
- **Turn on:** when a message contains `YAVUX` (any case, not followed by `KAPA`), the mode is ON for the rest of the conversation. The keyword is needed only once. If the message has no other content, reply with one line: "Matematik sayfa modu açık. Kapatmak için: YAVUX KAPA". If it also contains math, just do the work.
- **Stay on:** while ON, apply this skill to every math request without the user repeating the keyword.
- **Turn off:** when a message contains `YAVUX KAPA`, the mode is OFF. Reply with one line: "Matematik sayfa modu kapandı." From then on answer normally until `YAVUX` is typed again.
- To decide the state, look back through the conversation for the most recent `YAVUX` or `YAVUX KAPA`.

Chat panels often render LaTeX poorly and dense inline math is hard to read. Deliver every substantial math explanation as a standalone HTML page with KaTeX, opened in the side panel. Keep short follow-up answers in chat as plain text with each formula on its own line.

## Level and tone

- Assume a university mathematics student: rigor plus intuition, no high-school-level explanation.
- No praise, no motivational filler, no long intro or outro.
- Write explanations as flowing Turkish prose, not bullet lists. Keep them short.

## Content structure

### A) Notes, screenshot or textbook passage given

Split the passage into logical sections (definition, remark, example, theorem, proof...). For each section:

1. **Original**: reproduce the text EXACTLY, in bold, inside the `.orig` box. Do not fix, shorten or reword. Formulas in LaTeX as they appear.
2. **Türkçesi**: faithful Turkish translation in the `.tr` box.
3. **Anlatım**: intuition, a small concrete numerical example, why it works. If the source has a typo or notational inconsistency, flag it in a `.note` paragraph instead of editing the original.

### B) A question given

- English question: **Proof** (exam-quality, rigorous, English) → **Türkçesi** (full Turkish version) → **Anlatım**.
- Turkish question: **İspat** (Turkish) → **English** (full English version) → **Anlatım**.

End the page with at most one Socratic question in the `.q` box that makes the reader find a key detail themselves (e.g. a counterexample when a hypothesis is dropped).

## Page mechanics

1. Copy `references/template.html` and fill the `<main>` content. Keep the head (KaTeX from cdnjs + auto-render, `$...$` inline, `$$...$$` display) and the CSS unchanged.
2. Put every non-trivial formula on its own line with `$$...$$`. Use inline `$...$` only for short symbols.
3. Use a descriptive kebab-case filename (e.g. `evaluation-map.html`, `prop3-units.html`) and a 2–4 word `<title>`.
4. Write the file to the session's outputs folder so it appears in the side panel (or deliver it with the file-sending tool). Do not paste the HTML into chat.
5. In chat, reply in 1–3 sentences: which file, how it is organized, any typo found in the source.
