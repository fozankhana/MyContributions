# my-contributions

A log of open source contributions.

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
