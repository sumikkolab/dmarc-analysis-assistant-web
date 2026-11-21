# DMARC Analysis Assistant

**Can this domain move to p=reject? If not, what is causing the failures, and what should you do?**

[日本語版 README](README_ja.md)

This README is for version 1.1.1.0. The reject readiness screen and the forwarding impact view are features of 1.1.0.0 and later.

## What is this tool?

DMARC Analysis Assistant is a Windows desktop tool that imports DMARC aggregate reports (XML / ZIP / GZ) and related bounce messages, and shows whether a domain can move its DMARC policy to p=reject. If it cannot, the tool shows what is causing the failures and what to do next.

Analysis results are stored on your PC and are not sent to external AI or cloud analysis services.

## Readiness for reject

Open "Readiness for reject" in the left menu after importing reports.

- **Verdict (four values):** Ready to move / Conditional (action needed) / Not ready / Not enough information to decide
- **Pass-rate gauge:** marks at 75%, 90%, and 99%. **These band values are operational guidelines (no official basis).**
- **Recommended actions:** the next step consistent with the verdict. The screen recommends changing to reject only when the verdict is "Ready to move".
- **Expected rejections if you move to reject:** broken down into authentication failures from your own senders, pending review, possible spoofing, and possible forwarding, as a range from the minimum (possible spoofing only) to the maximum (all messages that fail DMARC).
- **Basis for the decision:** official items (RFC 9989 / RFC 9990, Microsoft and Google documents, with sources) are separated from operational guidelines.
- **Impact of forwarding:** the pass rate for all messages and excluding possible forwarding, with the number of excluded messages. Failing forwarding sources can be registered as forwarding servers.

## Classification

Each record is classified by a deterministic rule-based engine, using the DMARC result, the exception reasons reported by receivers, and the IP ranges you register on the settings screen. Registered settings apply from the next analysis; mailbox import and the CLI use the same settings.

| Category | Condition |
|----------|-----------|
| **OK** | DMARC passes. |
| **Authentication failures from your own senders** | DMARC fails and the source IP is within the own mail server IP ranges you registered. |
| **Possible forwarding** | DMARC fails and the source IP is within a registered forwarding server range, or the receiver reported `trusted_forwarder` or `mailing_list`. |
| **Spoofing suspected** | DMARC fails and none of the above applies. |
| **Pending review** | DMARC fails, none of the above applies, and the source matched a known sending service. The current settings screen has no field to register these, so this is normally not assigned. |

## Key features

- Reads DMARC aggregate reports (XML / ZIP / GZ) from a folder or a Microsoft 365 shared mailbox
- Dashboard, DMARC Records list, and a summary by sending server and by domain
- Bounce message analysis (Microsoft 365 or a local EML folder), separate from DMARC classification
- Technical and executive PDF reports, Excel, and CSV export
- Management tags (Managed / Monitored / External) per domain; they do not affect classification or totals
- Japanese / English UI

## Privacy & Security

- Analysis results are stored on your PC and are not sent to external AI or cloud analysis services
- Microsoft 365 connections are made only when you configure them
- Fetching from the app screen uses only the read permission `Mail.Read.Shared` and never deletes, moves, marks as read, or sends mail.- Authentication tokens are held in memory only and are never persisted to disk
- Telemetry, crash reports, and usage history are **not collected**
- Stored data lives under `%LocalAppData%\DmarcAnalysisAssistant` and can be deleted by the user
- Consent required on first launch; re-consent on terms update

## System requirements

- Windows 10 / 11
- .NET 10 (included with the Store package)
- Microsoft Edge WebView2 Runtime
- Microsoft 365 Graph API access (only if using the optional mail import feature)

## Links

- [Product site](https://dmarc-analysis.sumikkolab.com/)
- [Manual](https://dmarc-analysis.sumikkolab.com/manual/)
- [Privacy Policy](https://dmarc-analysis.sumikkolab.com/privacy-policy.html)
- [Terms of Use & Disclaimer](https://dmarc-analysis.sumikkolab.com/terms-of-use.html)
- [Support](https://dmarc-analysis.sumikkolab.com/support.html)

## Disclaimer

Classifications, verdicts, and inferences shown by this tool are rule-based analyses derived from report contents and mail headers. They do not confirm sender intent or actual DNS configuration. Labels such as "Spoofing suspected", "Authentication failures from your own senders", and "Possible forwarding" are machine-produced estimates and may not classify every case correctly. The final judgment rests with the user.

---

© 2026 Sumikko Lab
