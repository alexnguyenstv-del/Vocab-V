# Japanese Learning Hub — Rebuild V2

A fresh static HTML/CSS/JavaScript learning workspace for GitHub Pages. No backend or build step is required. Learning data is stored in the browser's LocalStorage.

## Deploy
Upload `index.html`, `styles.css`, `app.js`, and this README to the repository root, then enable GitHub Pages from the main branch and `/ (root)`.

## Implemented in this rebuild
- Dashboard and sidebar navigation.
- Vocabulary Inbox with 7-field bulk import, preview, duplicate checks, search, edit and delete.
- Vocabulary Boxes: create flow immediately opens a Grid word picker, All Imported / Recent Imported filters, Select All / Deselect All, and multi-select membership editing.
- Study inside each Vocabulary Box: Flashcard (tap to reveal; mark Known / Need Review) and Reading Recall (type Japanese with IME; Hiragana or the matching Kanji is accepted). Reading Recall supports 1–5 attempts, Enter submission, answer reveal, Enter/Next advance and retry incorrect. Kanji meaning study remains available in Kanji Boxes.
- Kanji Library auto-extraction from saved vocabulary, searchable cards and detail modal.
- Kanji Boxes with multi-select and Kanji meaning study.
- Dictionary autocomplete over built-in starter records, user vocabulary and imported dictionary JSON packs; save to Inbox, Box and Kanji Library.
- JSON backup and restore.
- Handwriting canvas removed.

## Important dictionary-data limitation
This ZIP **does not contain the full JMdict or KANJIDIC2 datasets**. The build environment used for this rebuild could not retrieve the upstream dataset files, so it would be misleading to describe the current offline dictionary as complete. The app includes a small starter vocabulary set and supports importing a prepared JSON dictionary pack through Settings. A full production offline dictionary requires bundling a properly converted JMdict + KANJIDIC2 data pack, with its licence and attribution files.

Suggested dictionary pack shape:

```json
{
  "words": [
    {
      "jp": "私",
      "kana": "わたし",
      "romaji": "watashi",
      "en": "I; me",
      "vi": "tôi",
      "pos": "pronoun",
      "examples": ["私は学生です。"]
    }
  ]
}
```

## Dictionary sources and licence
JMdict and KANJIDIC2 are maintained by the Electronic Dictionary Research and Development Group (EDRDG). Their dictionary files are made available under CC BY-SA 4.0 with EDRDG attribution and other licence conditions. See:
- https://www.edrdg.org/dokuwiki/doku.php?id=start
- https://www.edrdg.org/edrdg/licence.html

Any bundled derivative database must preserve required attribution and compatible ShareAlike terms. Vietnamese glosses in the app are separate curated data; do not treat automatically generated translations as authoritative.

## Import vocabulary format
One word per line, exactly seven fields separated by `|`:

```text
Japanese | Hiragana | Romaji | English meaning | Vietnamese meaning | Part of speech | Example sentence
私 | わたし | watashi | I; me | tôi | pronoun | 私は学生です。
```

## Notes
- This is a functional rebuild, but it has not yet undergone full end-to-end browser QA in Chrome. Please test the listed flows before relying on it as your only copy of study data.
- Export a backup regularly. Clearing browser data can erase the local workspace.
