# SecurityCyber CTI Feed

**Free, open threat intelligence for defenders — TAXII 2.1 / STIX 2.1.**
No paywall, no sign-up, no vendor bias. Inquest, not judgment.

SecurityCyber publishes atomic indicators (IPv4, URLs, domains, file hashes) from
its own cloud-hosted honeypots and verified CTI. The feed is designed to drop
straight into a SIEM or a TI platform with a native connector — no custom code.

## Access

### TAXII 2.1 (live, recommended)
- **Discovery / API root:** `https://cti.securitycyber.uk/taxii2/`
- **Collection:** `indicators`
- **Objects:** `https://cti.securitycyber.uk/taxii2/api/collections/indicators/objects/`
- Anonymous, read-only. Supports `?added_after=<timestamp>` and `?limit=` for incremental polling.

Connect it with the **native** connector in your platform:
- **Microsoft Sentinel** — *Threat Intelligence – TAXII* data connector (API root URL above, collection `indicators`).
- **Splunk** — a TAXII 2.1 input (Enterprise Security / Threat Intelligence Management, or a TAXII TA).
- **MISP** — add a TAXII 2.1 feed pointing at the API root.
- **OpenCTI** — the TAXII 2.1 connector.

### Static STIX bundle (this repo)
`data/indicators.stix.json` — a STIX 2.1 **bundle** of the current indicators,
refreshed from the live feed. Clone or `git pull` and import it directly into
MISP / OpenCTI, or use it in any tooling that reads STIX 2.1.

## Format

STIX 2.1 `indicator` objects with `pattern_type: "stix"`, e.g.:

```json
{
  "type": "indicator",
  "spec_version": "2.1",
  "id": "indicator--…",
  "pattern": "[ipv4-addr:value = '203.0.113.45']",
  "pattern_type": "stix",
  "valid_from": "…",
  "labels": ["malicious-activity"],
  "external_references": [{ "source_name": "SecurityCyber", "url": "https://cti.securitycyber.uk/" }]
}
```

Patterns cover `ipv4-addr`, `url`, `domain-name`, and file hashes
(`SHA-256` / `SHA-1` / `MD5`). Values are **real, not defanged** — this is a
detection feed meant to be matched on. Private/reserved IPs and `.onion`
addresses are excluded by design.

## Scope & caveats
- First-party honeypot telemetry plus verified public CTI. Treat it as one input
  among several, not ground truth.
- Best-effort, as-is, no warranty. If you spot a false positive, open an issue.

## Licence
The indicator **data** in this repository is released into the public domain
under **CC0 1.0** (see [`LICENSE`](LICENSE)) — use it freely, no attribution
required (though a mention is always welcome). The SecurityCyber platform code
itself is separate and not covered by this licence.

## About
Run by Charlie Collins / SecurityCyber — a free, defender-first CTI platform.
<https://cti.securitycyber.uk/> · <https://securitycyber.uk/>
