# Draft Inbox

Use this directory to preserve authentic ideas, questions, and requests from before they are discussed. They do not need to be complete or mature.

- For personal or low-concurrency use, the recommended filename is `YYYYMM.md`, such as `202611.md`. For parallel collaboration, use `YYYYMM_author.md`, such as `202611_lqf.md`, with a stable team account or author identifier. Separate author files allow independent numbering and avoid shared-file merge conflicts.
- Group entries under `YYYY-MM-DD` headings and number them `01`, `02`, and so on within that date, with a short topic heading:

  ```markdown
  ## 2026-11-18

  ### 01 Export format

  Could we support both JSON and CSV exports?
  ```

  The date is when the entry was captured, not when the idea first occurred. Keep entry numbers stable; do not renumber, rearrange, or move unresolved entries into a new month. One file may contain many topics and remain open across later months.
- Preserve the author's original wording. An agent capturing an idea or receiving a draft without this metadata should use the actual capture date, append the next number within that date, and add a short heading rather than asking the author to rewrite the input. Do not infer an earlier idea date from file timestamps. For historical material, use the actual import date and identify it as imported on that date, or state that its original date is unknown.
- Source references identify the file, entry date, number, and topic scope, for example `Drafts/202611.md (2026-11-18 / 01 / Export format)`. In per-author files the path already establishes authorship, so the entry number needs no author prefix.
- Legacy `YYYYMMDD_sequence.md` files and their Source references remain valid. Do not rename or rewrite them merely to adopt monthly drafts. A project may choose another deliberate convention as long as entries remain stably identifiable and traceable.
- Images are allowed. A suggested location is `Drafts/Images/`, referenced with relative paths.
- A draft is not a confirmed requirement. Undiscussed and unconfirmed content remains pending. The index, rather than the newest monthly file, determines pending work.
- When adding a draft entry, also list its pending topics in `../Progress/Progress.md`. Before a decision record exists, use `—` in the Record column and “Pending discussion” as the status.
- Do not delete an original draft after one of its topics is confirmed and archived. Archiving creates a separate decision record; it does not move the draft. Keep any remaining topics pending in the index.
- Conclusions raised directly in conversation do not require a draft to be added here afterward.

You may remove this guide once contributors are familiar with the workflow, provided the merged `AGENTS.md` still covers pending-topic indexing and draft preservation and the project has another deliberate way to retain the otherwise empty `Drafts/` directory in Git.
