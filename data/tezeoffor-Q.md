### [L-1] Dangerous strict equality in `VaultManagerV2::withdraw` can cause manipulation by attacker (Root Cause -> Impact)

**Description:**
Use of strict equalities that can be easily manipulated by an attacker.

**Impact:**

Miners can manipulate the `block.number` and always cause revert

**Recommended Mitigation:**

Don't use strict equality to determine if an account has enough Ether or tokens.