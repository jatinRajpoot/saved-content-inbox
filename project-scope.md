# Saved Content Inbox - Project Scope

Build a local browser inbox that makes saved web and social content searchable across sources and preserves the information actually captured. The first release proves useful retrieval before investing in fragile platform integrations.

## Users and problem

People with hundreds of saved articles, posts, and videos struggle to find material spread across platform-specific lists. Target users maintain at least 500 saves and regularly need to find something they saved weeks earlier.

## MVP workflow

1. Save the current page or visible post using the extension.
2. Review its captured title, URL, excerpt, platform, and optional thumbnail.
3. Search the local inbox and filter by source, creator, age, status, or available duration.
4. Move an item into Read, Watch, Buy, Cook, Visit, or Archive and reopen its source.
5. Export the library and restore it into a clean profile.

## Included in the MVP

- User-initiated capture for ordinary pages and accessible visible content, with editable metadata and capture-status feedback.
- Local full-text search over titles, captured text, notes, and tags; source and workflow filters.
- URL normalization, duplicate review, merge controls, and preservation of previously captured content.
- A unified inbox, user-defined collections, notes, handled/archive state, and simple forgotten-save resurfacing.
- Versioned portable export/import of metadata and captured assets, with partial-failure reporting.
- A staged YouTube Watch Later importer: first test an explicit user-provided export or user-authorized visible-page flow; ship only after reliability and platform requirements are checked.
- Source availability and capture timestamps; distinguish a saved URL from an offline text snapshot.

## Deferred features

Automatic Instagram, X, Reddit, and other platform synchronization, full media downloads, semantic embeddings, cross-device sync, team libraries, and paid automation are deferred. The MVP does not bypass logins, access controls, or unavailable content, and cannot preserve material it never captured.

## Proposed architecture and data

Use TypeScript with one extension framework such as WXT, a small UI, IndexedDB/Dexie, and Web Workers for indexing and imports. Start with a deterministic full-text index; consider SQLite-WASM only if collection size justifies it. Keep capture adapters separate from storage, search, and library workflows.

Persist SavedItem, CapturedSnapshot, SourceMetadata, Collection, Tag, and ImportJob entities. Maintain original and canonical URLs, source identifiers, capture timestamps, optional creator/duration metadata, and snapshot completeness. Upserts must never erase a valid local snapshot just because the original becomes unavailable.

## Privacy, permissions, and cost

Capture only at user action or within a specifically authorized import. Use optional site access, avoid password or cookie collection, and keep content and search indexes local. Provide per-item deletion and full-library erase. Treat captured HTML as untrusted and sanitize it before display. Exported libraries can contain private material and must be labeled accordingly.

Search and stored-content retrieval must work offline without developer-hosted accounts, paid AI, or a required server. Fetching new source content still needs internet access. User-owned encrypted sync and static documentation can be evaluated later.

## Acceptance criteria

- Captured title, URL, and available text remain searchable and readable after the source is unavailable.
- A 10,000-item fixture can be indexed and filtered without blocking the interface; record timings on a named reference machine.
- Repeated capture and repeated imports do not multiply identical items or erase existing notes.
- Missing creator, thumbnail, or duration values do not break filtering or item display.
- Interrupted imports can resume or safely retry with an item-level error report.
- Export/import into a clean profile preserves snapshots, notes, collections, and handled state.
- Scripted or malicious captured content cannot execute in the inbox.
- The interface clearly labels unsupported imports and incomplete snapshots.

## Delivery and validation

| Phase | Deliverable | Exit condition |
|---|---|---|
| 1 | Universal capture and local inbox | Users can save and retrieve ordinary web content. |
| 2 | Search, filters, deduplication, export | A large library round-trips and remains usable offline. |
| 3 | One validated importer and pilot | Imported saves produce repeated useful retrieval. |

Budget 6-10 solo-developer weeks as a planning estimate; integration fragility is the largest uncertainty. Recruit people with 500+ saves and measure weekly searches, reopened old items, handled items, and repeat use after the initial import. Add more platform adapters only if retention supports the effort. Future paid options include bulk import, richer snapshots, local semantic search, and user-owned sync.

## Scope basis

This scope is derived from the supplied report, "Recent Verified User Pain Points Suitable for Zero-Backend SaaS, Mobile Apps, and Browser Extensions" (research window ending November 3, 2026). Market demand, estimates, and monetization are hypotheses to validate; the report's internal citation markers are not independently verified references. This repository starts with this scope document only; implementation has not started.
