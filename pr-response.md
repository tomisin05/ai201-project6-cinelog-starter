# PR Response Doc — CineLog Watchlist Feature

## AI Usage
<!-- Fill in at the end — how you used AI tools during this project -->

## Comment 1 — Rename
**What I did:** Renamed `save_to_watchlist()` to `add_to_watchlist()` in `services/watchlist_service.py` to match the `verb_to_noun` convention used by `add_to_collection()`, `remove_from_collection()`, and `get_collection()`. Updated the import and call site in `routes/watchlist/watchlist.py` — confirmed those were the only two locations by searching the full project for `save_to_watchlist`.
**How I verified:** `pytest tests/ -v` passes. Grepped for `save_to_watchlist` — no remaining references.

## Comment 2 — Deduplication
**What I did:** Added `AlreadyInWatchlistError` exception class and a duplicate check to `add_to_watchlist()`, following the identical pattern used in `add_to_collection()`: query for an existing `WatchlistEntry` with the same `(user_id, film_id)` before inserting, and raise the named exception if one is found. Also updated the docstring to document the new exception.
**How I verified:** `test_add_to_watchlist_duplicate_raises` confirms only one entry exists after two add attempts and that the exception is raised on the second call. `pytest tests/ -v` passes.

## Comment 3 — Missing test
**What I did:** Created `tests/test_watchlist.py` with three tests mirroring the structure of `test_collection.py`: `test_add_to_watchlist_nonexistent_film_raises` (the specific test the reviewer flagged), `test_add_to_watchlist_creates_entry` (happy path), and `test_add_to_watchlist_duplicate_raises` (deduplication). Used the same `app`/`sample_user`/`sample_film` fixture pattern and `with app.app_context()` wrapping.
**How I verified:** `pytest tests/test_watchlist.py -v` — all three tests pass.

## Comment 4 — Default visibility
**My position:**
**Reasoning:**
**Tradeoff acknowledged:**

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
