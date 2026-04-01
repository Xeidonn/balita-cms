# balita-cms

A lightweight editorial CMS with role-based workflow and automatic English-to-Filipino translation. Built as a challenge submission for an internship application.

---

## What It Does

Balita CMS handles the full editorial pipeline in a single HTML file — no build step, no server required. Writers submit articles in English, a translation preview is generated automatically, and a separate reviewer role approves (with edits) or rejects before publishing.

**Flow:** Login → Write article → Auto-translate to Filipino → Submit → Reviewer edits translation → Approve & Publish

---

## Features

- **Role-based login** — Editor and Reviewer accounts with separate views and permissions
- **Auto-translation** — Triggers automatically on paste (800ms debounce) with a 3-API fallback chain: MyMemory → Google Translate (unofficial) → LibreTranslate
- **Inline translation editing** — Reviewers can correct the Filipino text directly before publishing
- **Reject with feedback** — Rejected articles return to the editor with a written reason
- **Bilingual reader view** — Published articles toggle between English and Filipino
- **Persistent storage** — Articles survive page refresh via `localStorage`

---

## Demo Credentials

| Role     | Username   | Password    |
|----------|------------|-------------|
| Editor   | `editor`   | `editor123` |
| Reviewer | `reviewer` | `review123` |

---

## Running Locally

No dependencies. Just open the file:

```bash
# Option 1 — direct browser open
open prototype.html

# Option 2 — local server (recommended, avoids browser CORS restrictions on fetch)
npx serve .
# then open http://localhost:3000/prototype.html
```

> **Note:** The auto-translation relies on external APIs. Opening via `file://` in some browsers blocks cross-origin requests. Use a local server if translation isn't working.

---

## Project Structure

```
balita-cms/
├── prototype.html     # Full application (single file)
├── design_note.docx   # 1-page design note explaining approach and decisions
└── README.md
```

---

## Technical Decisions

**Translation API** — Uses a fallback chain so translation works even if one provider is rate-limited. No API key required for any of the three.

**Storage** — `localStorage` for the prototype. The article data model (`id`, `title`, `body`, `translatedBody`, `status`, `author`, timestamps) is structured for a direct migration to a Node.js + PostgreSQL backend.

**Auth** — Hardcoded credentials in the prototype. Production path: JWT sessions + bcrypt + role middleware on API routes.

**Single file** — Intentional for the challenge submission. Easier to review, zero setup friction for the evaluator.

---

## What's Next (Production Path)

- Node.js + Express REST API
- PostgreSQL with Sequelize or Prisma ORM
- JWT authentication with role-based route guards
- DeepL or Google Cloud Translation API for higher accuracy
- Rich text editor (TipTap or Quill) replacing the plain textarea
- Email notifications to reviewers on new submissions

---

## Author

**Myles Ramirez** — BS Information Technology, De La Salle University  
[github.com/Xeidonn](https://github.com/Xeidonn) · [linkedin.com/in/myles-ramirez-6b29a632b](https://linkedin.com/in/myles-ramirez-6b29a632b)
