---
description: This is a list of the available client side exports.
---

# Client Exports

## GetInsuranceStatus

```lua
-- This will return true/false if a player is insured

exports.MrNewbPrescriptions:GetInsuranceStatus()
```

## ReturnInsuredRate

```lua
-- This will return a rate based on the copay percentage set in config
-- passing a value will do some math and if player is insured return a lower price

exports.MrNewbPrescriptions:ReturnInsuredRate(amount)
```

## StopEffects

<pre class="language-lua"><code class="lang-lua">-- This export will stop drug effects set by this script
<strong>exports.MrNewbPrescriptions:StopEffects()
</strong></code></pre>
