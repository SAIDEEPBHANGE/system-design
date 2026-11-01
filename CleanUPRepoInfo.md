# File-Level Cleanup Completed

This table records the individual files removed from the approved list. No folders were deleted.

| File name | Repository path | Action | Reason for removal |
|---|---|---|---|
| `00-README.md` | `Github-Primer/00-README.md` | Removed | This was an overview of the summarized course; its study-order entries referred to course files no longer present in the current folder structure. |
| `.gitignore` | `Github-Primer/system-design-primer-master/.gitignore` | Removed | This copied Python development ignore file covered build artifacts and Python files; the current Primer tree contains no Python source or notebooks. The root `.gitignore` remains. |
| `.gitattributes` | `Github-Primer/system-design-primer-master/.gitattributes` | Removed | Its only rule labeled Jupyter notebooks as Python, but the current Primer tree contains no notebooks. |
| `CONTRIBUTING.md` | `Github-Primer/system-design-primer-master/CONTRIBUTING.md` | Removed | It documented how to contribute to the upstream Primer, not system-design concepts. Its contribution links and section were also removed from the retained English `README.md`. |
| `epub-metadata.yaml` | `Github-Primer/system-design-primer-master/epub-metadata.yaml` | Removed | It supplied metadata for generating an EPUB; the EPUB-generation script is absent from the current folder structure. |
| `README-ja.md` | `Github-Primer/system-design-primer-master/README-ja.md` | Removed | Japanese translation of the retained English Primer; this copy is being kept English-only. Its local link was removed from the English README. |
| `README-zh-Hans.md` | `Github-Primer/system-design-primer-master/README-zh-Hans.md` | Removed | Simplified Chinese translation of the retained English Primer; this copy is being kept English-only. Its local link was removed from the English README. |
| `README-zh-TW.md` | `Github-Primer/system-design-primer-master/README-zh-TW.md` | Removed | Traditional Chinese translation of the retained English Primer; this copy is being kept English-only. Its local link was removed from the English README. |
| `TRANSLATIONS.md` | `Github-Primer/system-design-primer-master/TRANSLATIONS.md` | Removed | It tracked translation maintainers and contribution status rather than teaching system design. The translation-help link was also removed from the English README. |
| `OO Design.apkg` | `Github-Primer/system-design-primer-master/resources/flash_cards/OO Design.apkg` | Removed | This deck was for object-oriented design exercises rather than system design. The two system-design flashcard decks were retained. |
