# 3nglish with 3li — progress board

A private, encrypted status board for the 3nglish with 3li estate: every project, what it
contains, how far along it is, and what is outstanding.

**Every file here is ciphertext.** Each page is AES-256-GCM encrypted with a key stretched from
a password using PBKDF2-HMAC-SHA256 (300,000 iterations). The password is not in this repo and
is not recoverable from it — the pages are rebuilt if it is ever lost.

The board is generated, never hand-edited. Its source lives outside this repo, in
`Downloads\_STATUS\`:

| file | what it does |
|---|---|
| `scan.py` | measures pages, sheets, sizes and PDF freshness off the real files |
| `tasks_parse.py` | reads the open items out of `PENDING_TASKS.txt` |
| `ledger.py` | the declared state — phases, milestones, story sign-off |
| `build_status.py` | renders the site |
| `publish_github.py` | inlines the assets, encrypts every page, stages this folder |

To rebuild and republish:

```
py -3.12 "C:\Users\signu\Downloads\_STATUS\build_status.py"
py -3.12 "C:\Users\signu\Downloads\_STATUS\publish_github.py"
git -C "C:\Users\signu\Downloads\_STATUS\public" add -A
git -C "C:\Users\signu\Downloads\_STATUS\public" commit -m "Update board"
git -C "C:\Users\signu\Downloads\_STATUS\public" push
```

Note: decryption uses WebCrypto, which requires a secure context. The board works over
`https://` and over `http://localhost`, but not by opening a file directly from disk.
