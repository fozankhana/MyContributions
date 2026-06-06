# My Contributions:

A log of open source contributions.

---

## [projectsend](https://github.com/projectsend/projectsend) — Security vulnerability fixes & code quality improvements

**Fork:** https://github.com/fozankhana/projectsend  
**Commit:** 6047e5c  
**Date:** 2026-06-06

### What was fixed

**Security vulnerabilities:**

| Severity | File | Issue Fixed |
|----------|------|-------------|
| Critical | `includes/Classes/Auth.php` | **LDAP Injection** — email was interpolated directly into LDAP filter `(mail=$email)`; fixed with `ldap_escape($email, null, LDAP_ESCAPE_FILTER)` |
| High | `includes/Classes/Download.php`, `includes/functions.php` | **CRLF Header Injection** — `filename_original` written into `Content-Disposition` header without stripping `\r\n`; fixed by stripping CR/LF in `sanitize_filename_for_download()` and at all inline header sites |
| High | `includes/functions.php` | **IP Spoofing bypasses brute-force** — `get_client_ip()` trusted `X-Forwarded-For` over `REMOTE_ADDR`, letting attackers forge any IP; rewritten to always return `REMOTE_ADDR` first |
| Medium | `assets/src/js/parts/side_modal.js` | **DOM-based XSS** — `setTitle()` used `innerHTML`; switched to `textContent` |
| Medium | `includes/Classes/Users.php` | **Weak hash validation** — `strlen($hash) >= 20` could accept broken hashes; replaced with `password_get_info()` algo check |
| Medium | `includes/Classes/BruteForceBlock.php` | **SQL string concatenation** — `time_frame_minutes` concatenated into both SELECT and DELETE queries; cast to `(int)` before interpolation |
| Low | `includes/Classes/RememberMe.php` | **Dead security enforcement** — token revocation on user-agent mismatch was logged but commented out; enabled `revokeToken()` + `return false` |

**Code quality:**

| File | Change |
|------|--------|
| `includes/functions.php` | Removed `shell_exec`/`exec` path from `get_real_size()`; `filesize()` is sufficient. Removed orphaned `isEnabled()` helper. |
| `includes/core.update.php` | Deleted commented-out `mysql_query()`/`mysql_fetch_array()` block (functions removed in PHP 7, unreachable dead code) |

---

## [system-design-primer](https://github.com/donnemartin/system-design-primer) — Bug fixes & translation sync

**Fork:** https://github.com/fozankhana/system-design-primer  
**Commit:** b59489b  
**Date:** 2026-06-05

### What was fixed

**OOP solution Python files & notebooks:**

| File | Bug Fixed |
|------|-----------|
| `solutions/object_oriented_design/call_center/call_center.py` | `super(Operator, self)` copy-paste error in `Supervisor` and `Director` classes; missing `call_center` parameter in all three subclass constructors; `NotImplemented` → `NotImplementedError` |
| `solutions/object_oriented_design/lru_cache/lru_cache.py` | `self.next = next` shadowed Python builtin → `self.next = None`; added missing `self.prev = None` |
| `solutions/object_oriented_design/online_chat/online_chat.py` | `PrivateChat.__init__` called `super().__init__()` without required `chat_id` argument; added missing `from enum import Enum` import |
| `solutions/object_oriented_design/parking_lot/parking_lot.py` | `self.spot_size` (bare expression, never assigned) → `self.spot_size = spot_size`; added `from enum import Enum`; fixed `LARGE`/`COMPACT` → `VehicleSize.LARGE`/`VehicleSize.COMPACT`; fixed `for level in levels` → `for level in self.levels` |

All four corresponding `.ipynb` notebooks were updated to match.

**Translation sync (3 files):**

Added 2 missing interview question rows to `README-zh-TW.md`, `README-zh-Hans.md`, and `README-ja.md` that existed in the English README but were never synced:
- *Design an API rate limiter*
- *Design a Stock Exchange (like NASDAQ or Binance)*
