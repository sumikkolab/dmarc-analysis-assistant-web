# DMARC Analysis Assistant

**DMARC reports, reclassified so you see what to fix.**

[日本語版 README](README_ja.md)

## What is this tool?

DMARC Analysis Assistant is a Windows desktop tool that analyzes DMARC aggregate reports (RUA) and related bounce messages **entirely on your local device**, classifies each entry into six categories, and makes it clear which rows need action and which can be safely ignored.

This is not a cloud service. Report contents, IP addresses, authentication results, and domain information are never transmitted externally.

## Why this tool exists

DMARC aggregate reports arrive as XML and list source IPs, SPF/DKIM results, and counts — but they don't tell you which entries are:

- **Spoofing suspicions** that need investigation
- **Configuration issues** in your own legitimate sending paths
- **Forwarded traffic** that can usually be ignored

This tool applies a deterministic, rule-based classification so operators can spend their time on real problems, not on reading XML.

## What this tool does

### Workflow: Import → Parse → Classify → Review → Export

| Step | What it does |
|------|-------------|
| **Import** | Load DMARC aggregate reports (XML / ZIP / GZ) from a folder, or fetch from Microsoft 365 inbox (optional) |
| **Parse** | Extract source IP, authentication results (SPF/DKIM), count, policy evaluations, and header metadata |
| **Classify** | Apply a six-category rule-based engine to each entry |
| **Review** | See entries as a list with filters, plus per-domain / per-category trends over time |
| **Export** | Export classification results to CSV for further analysis in Excel or BI tools |

### Six classification labels

| Label | Meaning |
|-------|---------|
| **Spoofing suspected** | Both SPF and DKIM fail, originating from external IP. Highest priority. |
| **Config issue** | Legitimate sender failing auth — DNS or sending path needs review. |
| **Forwarded** | Failure caused by forwarding. Usually no action needed. |
| **Legitimate** | Pass. Kept for record. |
| **Bounce** | Correlated with matched bounce messages. |
| **Unknown** | Insufficient information for automatic classification. |

### Key features

- DMARC aggregate report analysis with ZIP / GZ / XML support
- Bounce message correlation to distinguish forwarded traffic from real issues
- Trend aggregation by domain, classification, and period
- CSV export for further analysis
- Full Japanese / English bilingual UI
- **All data stored locally** — no external server transmission
- Deterministic rule-based classification — no AI inference, no cloud analysis

## Privacy & Security

- The tool runs locally on your device
- Report contents, IP addresses, authentication results, and domain information are **never sent** to any external service
- Microsoft 365 integration is **optional** — enabled only when the user configures it
- Permission scope is limited to `User.Read` + `Mail.Read` (read-only — no send, delete, or edit)
- Authentication tokens are held in memory only and are never persisted to disk
- Telemetry, crash reports, and usage history are **not collected**
- Stored data lives under `%LocalAppData%\DmarcAnalysisAssistant` and can be deleted by the user at any time
- Consent required on first launch; re-consent on terms update

## System requirements

- Windows 10 / 11
- .NET 8 Desktop Runtime
- Microsoft Edge WebView2 Runtime
- Microsoft 365 Graph API access (only if using the optional mail import feature)

## Links

- [Product site](https://dmarc-analysis.sumikkolab.com/)
- [Manual](https://dmarc-analysis.sumikkolab.com/manual/)
- [Privacy Policy](https://dmarc-analysis.sumikkolab.com/privacy-policy.html)
- [Terms of Use & Disclaimer](https://dmarc-analysis.sumikkolab.com/terms-of-use.html)
- [Support](https://dmarc-analysis.sumikkolab.com/support.html)

## Disclaimer

Classifications, verdicts, and inferences shown by this tool are rule-based analyses derived from report contents and mail headers. They do not confirm sender intent or actual DNS configuration. Labels such as "Spoofing suspected", "Config issue", and "Forwarded" are machine-produced estimates and may not classify every case correctly. The final judgment rests with the user.

---

© 2026 Sumikko Lab
