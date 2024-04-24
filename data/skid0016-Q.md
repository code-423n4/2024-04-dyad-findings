### [I-1] `VaultManagerV2::burnDyad` does not follow CEI, which is not a best practice

It's best to keep code clean and follow CEI(Checks, Effects, Interactions).

```diff
-   dyad.burn(id, msg.sender, amount);
-   emit BurnDyad(id, amount, msg.sender);
```
In your code, the interaction (dyad.burn()) happens before changing the contract's state or emitting an event, which doesn't follow the CEI pattern. To make it follow CEI, you would rearrange the steps to ensure that the internal state changes and all checks are done before interacting with external contracts.

```diff
+   emit BurnDyad(id, amount, msg.sender);
+   dyad.burn(id, msg.sender, amount);
```