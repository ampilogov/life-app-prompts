# Life app prompts

Editable prompt templates used by [Life](https://github.com/ampilogov/Life).

- [Polish](prompts/polish.md) reorganizes a journal entry into its five existing sections.
- [Summarize](prompts/summarize.md) summarizes a journal period for ChatGPT.

Life downloads templates over HTTPS from this repository's `main` branch when
running or copying a prompt. Edit a file and commit it to `main` to update future
requests without rebuilding the app (GitHub's CDN may briefly cache updates).
Life saves the last valid download on the device for offline use. Each prompt
needs one successful download before it can be used offline. With no saved copy,
a download failure shows an error and allows retrying.

## Template contract (v1)

Keep each required placeholder exactly once:

| File | Required placeholders |
| --- | --- |
| `prompts/polish.md` | `{{journal}}` |
| `prompts/summarize.md` | `{{period}}`, `{{section_count}}`, `{{section_names}}`, `{{journal}}` |

Life inserts these values locally after downloading. `journal` includes the entry
metadata, sections, and tasks for polish, or the selected journal sections for
summarize. No journal content is sent to GitHub. Templates must be UTF-8 text,
at most 128 KiB, and contain no other `{{...}}` placeholders. Invalid downloads
never replace the last valid copy.

The polish output headings, order, dash bullets, and Capture List checkbox format
must stay compatible with Life's response parser. Changing that output contract
requires a corresponding app update. Keep repository files free of journal data,
credentials, or API keys.
