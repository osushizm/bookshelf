You are a product engineer and UI designer.

Your task is to design and implement a web service called “My Bookshelf”
using Go as the main backend language.

The goal is to create a stylish, clean, and easy-to-read bookshelf-style
profile page for book lovers — not a reading log SNS, but a self-introduction
through favorite books.

# 1. Service Overview
- Users create a “bookshelf” and register their favorite books.
- Each bookshelf can be shared publicly via a URL.
- The service is mainly for self-expression and profile extension for book lovers.
- UI must be modern, stylish, and mobile-friendly.
- Card-based layout with book covers as the visual focus.
- Social sharing (Twitter/X) with beautiful OGP previews is critical.

# 2. Functional Requirements (MVP)
## Bookshelf
- Free users can register up to 5 books per bookshelf.
- Clicking a book opens a detail view showing a short personal comment.
- Once completed, a bookshelf can be published with a public URL.

## URL Design
- Registered users: /{userID}/{slug}
- Guest users (no registration): /share/{16-character-random-alphabet}
- slug is user-defined, URL-safe, and must not collide with reserved words
  (e.g. "share").

## Book Metadata
- Users can search books by title or ISBN and select from results.
- Desired metadata:
  - Title
  - Author
  - Cover image URL
  - Optional description
- External APIs should be abstracted and replaceable.
  Candidates:
  - Google Books API
  - openBD
  - Rakuten Books API

## Study / Library Page (Future Feature)
- A personal page that aggregates multiple bookshelves.
- Example path: /u/{userID}
- Not required for MVP, but architecture should allow it later.

# 3. Non-Functional Requirements
- VPS-based deployment (Docker + Nginx + Go + DB).
- PostgreSQL preferred (SQLite acceptable for MVP, with migration in mind).
- Book cover images are referenced via external URLs initially.
- Security:
  - Password hashing (bcrypt or argon2)
  - CSRF protection
  - Input validation
- Logging and monitoring:
  - Structured logging (zap, slog, etc.)
  - Basic metrics-ready design
- OGP support:
  - title, description, og:image dynamically generated per bookshelf.

# 4. Design Requirements (Very Important)
- Generous whitespace, rounded cards, subtle shadows.
- Book covers are the hero elements.
- Calm color palette (white / light gray base).
- Grid layout that looks good with exactly 5 books.
  - Desktop: 5 columns or 3+2
  - Mobile: 2 columns
- Titles are truncated; full title on hover or detail view.
- Book detail opens via modal or dedicated page.

# 5. Technology Choices (Please Propose)
- Go web framework:
  - Chi / Echo / Gin
  - Choose one and explain why.
- Rendering strategy:
  - Server-side rendering vs SPA
  - Recommend the best approach for MVP speed.
- CSS strategy:
  - Tailwind CSS or handcrafted CSS
  - Optimize for fast development and visual quality.
- Database access:
  - sqlc / ent / gorm / database/sql
  - Recommend one with reasoning.
- Architecture:
  - Avoid over-engineering.
  - Keep layers separated enough for maintainability.

# 6. Required Output Format
Provide concrete details in the following structure:

A) System Architecture (text-based diagram is fine)
- Nginx, Go app, DB, external APIs

B) Project Directory Structure (Go)
- e.g. /cmd, /internal, /web, /migrations

C) Database Design
- Tables such as:
  - users
  - shelves
  - shelf_items
- Include columns, indexes, constraints.
- Must support guest-created shelves.

D) API Design
- Endpoints for:
  - Book search
  - Shelf creation
  - Shelf update
  - Public shelf fetch
  - Share URL generation

E) Screen / UI Design
- Pages and components:
  - Landing
  - Shelf creation
  - Shelf edit
  - Shelf public view
  - Book detail modal/page
- Include OGP behavior expectations.

F) Implementation Roadmap
- Phase 0 → MVP → Post-MVP
- What to build first, in what order.
- Testing and deployment steps.

G) Risks and Pitfalls
- URL collisions
- External image failures
- API rate limits
- Twitter/X sharing quirks
- OGP caching issues

Constraints:
- Be concrete enough to start implementation immediately.
- Prioritize MVP speed and simplicity.
- Avoid unnecessary complexity.