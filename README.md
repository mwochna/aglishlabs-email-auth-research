# aglishlabs-email-auth-research

Research tooling, email headers, and analysis data supporting the MSc dissertation:

**"Email Authentication Adoption and Spoofing Resistance Among Irish SME Domains: 
A DNS Measurement and Controlled Receiver Study"**

Atlantic Technological University (ATU) Donegal, 2026

---

## Overview

This repository contains the scripts, raw email headers, analysis workbooks, 
and domain data produced during an empirical study of email authentication 
adoption across 7,289 Irish-oriented domains and spoofing resistance across 
seven receiver platforms and seven authentication regimes.

The study comprised two artefacts:
1. A DNS measurement framework scanning SPF and DMARC records across four 
   Irish domain datasets
2. A controlled email delivery testbed built on self-hosted Mail-in-a-Box 
   infrastructure, transmitting 500 legitimate and spoofed messages with 
   full email header capture

---

## Repository Structure
```
/analysis/          — XLSX workbooks: headers analysis, regimes book, 
                      DNS reports for all five domain datasets
/domain-lists/      — Domain dataset documentation and methodology
/headers/           — Raw email headers (txt) from experimental runs,
                      organised by legitimate/spoofed and by receiver
/legitimate-delivery-reports/ — Delivery outcome reports for legitimate tests
/scripts/           — Bash scripts for legitimate sending (swaks) 
                      and spoofed sending (telnet/SMTP)
```

---

## Scripts

### Legitimate send — `scripts/swaks_spray.sh`
Automates sending of legitimate test messages across all receiver accounts 
using SWAKS (Swiss Army Knife for SMTP). Logs SMTP response codes and 
timestamps to CSV.

**Dependencies:** bash, swaks  
**Usage:**
```bash
export SMTP_PASS="your_password"
./swaks_spray.sh <regime> <count_per_receiver> <sleep_seconds>
# Example: ./swaks_spray.sh dmarc-reject 10 0.8
```

### Spoofed send — `scripts/spoofed_send_regime.sh`
Sends spoofed messages directly via SMTP using telnet, claiming to be 
from the legitimate sender domain while originating from the attacker 
simulation domain (wochna.ie).

**Dependencies:** sh, telnet  
**Usage:**
```bash
./spoofed_send_regime.sh <receiver_alias> "<regime_label>"
# Example: ./spoofed_send_regime.sh gmail "regime dmarc-reject"
# Aliases: gmail, hotmail, yahoo, mailru, proton, titan, 25mailst
```

---

## Authentication Regimes Tested

| Regime | SPF | DKIM | DMARC |
|--------|-----|------|-------|
| none | — | — | — |
| spf | ✓ | — | — |
| dkim | — | ✓ | — |
| spf+dkim | ✓ | ✓ | — |
| dmarc-none | ✓ | ✓ | p=none |
| dmarc-quarantine | ✓ | ✓ | p=quarantine |
| dmarc-reject | ✓ | ✓ | p=reject |

---

## Receiver Platforms Tested

Gmail · Outlook (Hotmail) · Yahoo Mail · Mail.ru · 
Proton Mail · Blacknight Titan (dmarclabs.eu) · 25 Mail St. (dmarclabs.org)

---

## Domain Datasets

Five datasets were used for DNS measurement. Full results including 
per-domain SPF and DMARC outcomes are published in `/domain-lists/`.

| Dataset | n | Source |
|---------|---|--------|
| Business.ie employer-focused | 2,834 | business.ie employer directory |
| Tranco-derived .ie | 3,272 | tranco-list.eu |
| DomainTyper Top .ie | 1,000 | domaintyper.com |
| Castlebar Chamber of Commerce | 90 | Chamber membership register |
| Westport Chamber of Commerce | 93 | Chamber membership register |

All domains are publicly registered. DNS records are public information. 
No personal data is included in the published datasets.

---

## Ethics

All experiments were conducted using accounts and infrastructure under 
the sole control of the researcher. Sender domain (aglishlabs.email) 
and attacker simulation domain (wochna.ie) were both registered and 
operated by the researcher. No real users were targeted. The study 
was conducted under ATU Donegal research ethics guidelines.

---

## Citation

If you use this tooling or data in your own research, please cite:

> Wochna, M. (2026). *aglishlabs-email-auth-research: Tooling and data 
> for "Email Authentication Adoption and Spoofing Resistance Among Irish 
> SME Domains."* GitHub. 
> https://github.com/mwochna/aglishlabs-email-auth-research

---

## License

MIT License — see [LICENSE](LICENSE) for details.
