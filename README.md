# Cerdigent — False positive certificate detection (Defender TI)

## Context

On 2026-05-03, a Microsoft Defender threat intelligence update incorrectly flagged legitimate certificate registry keys as malicious, generating spurious alerts under the name **Cerdigent**.

This query identifies `RegistryKeyCreated` events matching the two impacted certificate thumbprints, scoped to events **after the faulty TI push**, to distinguish real detections from noise introduced by the update.


## Impacted certificate thumbprints
| Thumbprint | Notes |
|---|---|
| `0563B8630D62D75ABBC8AB1E4BDFB5A899B24D43` | Flagged by faulty TI update |
| `DDFB16CD4931C973A2037D3FC83A4D7D775D05E4` | Flagged by faulty TI update |

---

## Usage

- Run in Defender XDR Advanced Hunting
- The `Timestamp` filter (`> 2026-05-03T04:00:00`) isolates events post-TI-update — adjust if the rollout time differs in your tenant
- Cross-reference `InitiatingProcessFileName` to confirm legitimacy of the creating process

---

## Notes

- This query is not a detection rule — it is a triage tool to review false positive volume
- If alerts have already been closed/suppressed in your tenant, results may be lower than expected
- Consider adding a suppression rule in Defender for these thumbprints until Microsoft issues a TI correction

---

## References

- Microsoft Defender XDR Advanced Hunting schema: `DeviceRegistryEvents`
- Alert name: Trojan:Win32/Cerdigent.A!dha
- Impacted update date: 2026-05-03
