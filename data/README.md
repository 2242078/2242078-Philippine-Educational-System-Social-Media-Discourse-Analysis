# Data

## `social_media_cleaned_anonymized.csv`
The final cleaned corpus used in the analysis: 970 public posts/comments about the Philippine educational system, collected with Apify and Python scripts.

| Platform | Rows |
|---|---|
| Facebook | 407 |
| Reddit | 289 |
| TikTok | 230 |
| YouTube | 33 |
| Instagram | 11 |

**Anonymization applied (all rows kept):**
- Removed author/username columns and post links.
- Replaced URLs, emails, `@mentions` and `u/` handles in text with placeholders (`[URL]`, `[EMAIL]`, `@[USER]`, `u/[USER]`).
- Replaced one private username that appeared inside text with `[USER]`. Public organizations and figures named in discussion (e.g., DepEd, universities, officials) are kept because they are part of the topic content.

| Column | Description |
|---|---|
| `row_id` | Row number in this file |
| `post_id` | Pseudonymous post identifier (comments with the same `post_id` belong to the same post) |
| `comment_text` | Comment text |
| `post_title` | Post title (may be empty) |
| `post_text` | Text of the parent post |
| `datetime` | Timestamp (partly missing) |
| `query` | Search query used for collection (empty for some rows) |
| `social_media_source` | Platform the row was collected from |

Verbatim public text can still be searched on the original platforms, and names typed in plain text (without an @) may remain in some Facebook comments. Use this data for research and reproducibility only, do not attempt to identify users, and respect each platform's terms.