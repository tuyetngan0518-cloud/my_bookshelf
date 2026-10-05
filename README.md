# BookShelf

A personal online library. Every book you have read sits as a cover on a shelf inside a 2D pixel-art ancient fantasy library, and you can share it with a link.

**Status:** the v1 specification is written. Implementation has not started yet. There is no demo link yet.

## v1 scope
- Add books one at a time or in bulk (paste up to 500 lines or upload a CSV)
- A pixel-art bookshelf where every book has a cover (looked up, generated or uploaded)
- A public share link for your library
- An AI reading summary: statistics are computed by code, and the language model only writes the narrative from those statistics
- An anonymous like/dislike feedback widget

## Why
I have read more than 300 books, mostly in Vietnamese and some in English, in print and on Kindle. I cannot keep them all on a shelf or a device, so I want a permanent memory of what I have read that I can share.

## Documentation
- [Product brief](docs/product-brief.md): vision, scope and non-goals
- [v1 specification](docs/v1-spec.md): the full build specification
- [AI coding rules](docs/ai-coding-rules.md): rules for the AI coding assistant

## Planned stack
Next.js (App Router), TypeScript in strict mode, Supabase, Vercel
