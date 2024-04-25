### [NC-01] Missing Event Emission in `setKeroseneManager()`, `KerosineManager::add()`,  `KerosineManager::remove()`, `BoundedKerosineVault::setUnboundedKerosineVault()`, `UnboundedKerosineVault::setDenominator()` functions.

**Description:** 
Absence of emitting an event within these functions `setKeroseneManager()`, `KerosineManager::add()`,  `KerosineManager::remove()`, `BoundedKerosineVault::setUnboundedKerosineVault()`, `UnboundedKerosineVault::setDenominator()`. Events are crucial for providing transparency and enabling external systems to react to state changes within the contract

**Impact:** 
The impact of this vulnerability is a lack of transparency and communication regarding changes 


**Recommended Mitigation:** 
Ensure that appropriate events are emitted within these functions.