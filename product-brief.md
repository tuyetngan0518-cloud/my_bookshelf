# BookShelf: Product Brief (v1)

## Vision and feel
BookShelf is a personal online library. Each user has one library. In v1 it shows every book the user has read as a cover on a shelf, inside a 2D pixel-art ancient fantasy library: old wooden shelves, warm light, a fairy-tale mood. A visitor should feel pulled in and impressed by a large collection and a beautiful space. In the long term all libraries live on a "book planet" where people visit each other's libraries and see what they have read. The planet and all community features are not in v1.

## Why
The founder has read 300+ books (physical and Kindle, mostly in Vietnamese, some in English) and cannot keep them all physically or on a device. The library is:
- a permanent memory of what they have read,
- a way to share it,
- a way to learn about other readers' taste and perspective.

## Wow moment
- A visitor who has read few books feels inspired and finds the owner interesting.
- A visitor who has read many books becomes curious about the owner's taste through an AI summary and wants to build their own library.

## v1 scope
- Add books one at a time or in bulk (paste lines or upload a CSV, up to 500 rows).
- Personal library shown as a pixel-art bookshelf. Every book always has a cover: a looked-up cover, a generated placeholder, or an uploaded photo.
- Each book has a lookup title (English or original edition, used for finding metadata and covers) and records the language the owner actually read it in. An optional title as read (for example the Vietnamese title) is display-only.
- Public share link.
- AI reading summary (statistics computed by code, narrative written by an LLM from those statistics only).
- Anonymous feedback widget (like or dislike of the idea, optional comment).

## Non-goals (not in v1)
Follow, like or comment on books; feed; notifications; messaging; groups; levels; streaks; the book planet; any theme other than the ancient fantasy theme.

## Constraints
One developer, 8 working hours per day, total budget 0 to 5 USD, free tiers only. Next.js (App Router) with TypeScript strict mode, Supabase, Vercel. Every LLM call is server-side and goes through one provider-agnostic function.

## Success criterion
The founder adds almost all books they have ever read, not just a few dozen. Measured as: at least 300 books saved in the founder's library within 30 days of launch. (DEFAULT, founder to confirm [D-33])

## Expansion trigger
The decision to expand beyond v1 depends on market reaction collected through the feedback widget. Measured as: at least 50 feedback votes, of which at least 60% are "like". (DEFAULT, founder to confirm [D-34])
