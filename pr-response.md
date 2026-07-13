# PR Response Doc — CineLog Watchlist Feature

## AI Usage
<!-- Fill in at the end — how you used AI tools during this project -->

## Comment 1 — Rename
**What I did:**
- Renamed the function `save_to_watchlist()` to `add_to_watchlist()` in [services/watchlist_service.py](file:///C:/Users/Erold%20Rayan/Downloads/AI201-Summer%20Program/Module%202/Week%206/ai201-project6-cinelog-starter/services/watchlist_service.py) to follow the project's `verb_to_noun` naming convention.
- Updated all call sites and import statements in [routes/watchlist/watchlist.py](file:///C:/Users/Erold%20Rayan/Downloads/AI201-Summer%20Program/Module%202/Week%206/ai201-project6-cinelog-starter/routes/watchlist/watchlist.py).

**How I verified:**
- Conducted a project-wide search (`grep`) for `save_to_watchlist` to confirm no remaining references to the old name exist.
- Ran the test suite using `pytest` to verify the codebase remains stable and functioning.

## Comment 2 — Deduplication
**What I did:**
- Defined a new custom exception class `AlreadyInWatchlistError` in [services/watchlist_service.py](file:///C:/Users/Erold%20Rayan/Downloads/AI201-Summer%20Program/Module%202/Week%206/ai201-project6-cinelog-starter/services/watchlist_service.py).
- Added logic in `add_to_watchlist()` to query the database for existing duplicate watchlist entries (`WatchlistEntry.query.filter_by(user_id=user_id, film_id=film_id).first()`) and raise `AlreadyInWatchlistError` if one is found.

**How I verified:**
- Verified that existing unit tests continue to pass successfully.

## Comment 3 — Missing test
**What I did:**
- Created [tests/test_watchlist.py](file:///C:/Users/Erold%20Rayan/Downloads/AI201-Summer%20Program/Module%202/Week%206/ai201-project6-cinelog-starter/tests/test_watchlist.py) containing tests for the watchlist service.
- Wrote three test cases mirroring the patterns in `test_collection.py`:
  1. Happy path: `test_add_to_watchlist_creates_entry`
  2. Duplicate handling: `test_add_to_watchlist_duplicate_raises` (asserts `AlreadyInWatchlistError`)
  3. Nonexistent film ID handling: `test_add_to_watchlist_nonexistent_film_raises` (asserts `FilmNotFoundError`)

**How I verified:**
- Ran the test suite via `pytest`, confirming all 7 tests (4 for collections, 3 for watchlist) pass successfully.

## Comment 4 — Default visibility
**My position:**
Watchlist entries should default to private (`public=False`) instead of public.

**Reasoning:**
Privacy by Design: User preferences and intents, such as saving a film to watch later, should remain confidential by default. Users should explicitly opt-in to share their watchlist data publicly rather than having their data exposed automatically without active consent.

**Tradeoff acknowledged:**
This decision may reduce spontaneous social discovery and sharing within the community, as many users tend to stick with default settings. However, protecting user privacy by default is a higher priority for user trust.

## Comment 5 — Sort order
**My position:**
**Reasoning:**
**Engagement with reviewer's point:**

## Comment 6 — Rebase
**What conflicted:**
**How I resolved it:**
**How I verified no conflict remains:**

## PR Description
<!-- Written at the end — feature overview, design decisions, manual testing steps -->