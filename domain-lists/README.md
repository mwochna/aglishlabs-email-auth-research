# Domain Lists

This folder contains the DNS measurement results for all five domain 
datasets used in the study. Each file includes the domain name alongside 
its observed SPF and DMARC configuration at the time of measurement 
(Q4 2025).

## Files

| File | n | Source |
|------|---|--------|
| report-business.ie-domains.xlsx | 2,834 | Business.ie employer directory |
| report-tranco-domains.xlsx | 3,272 | Tranco top-1M list (tranco-list.eu), filtered to .ie |
| report-domaintyper-domains.xlsx | 1,000 | DomainTyper Top .ie (domaintyper.com) |
| report-castlebar-chamber.xlsx | 90 | Castlebar Chamber of Commerce membership register |
| report-westport-chamber.xlsx | 93 | Westport Chamber of Commerce membership register |

## Methodology

DNS records were queried in Q4 2025 using a bulk domain analyser tool 
performing simultaneous SPF and DMARC record lookup across all domains. 
Each record captures SPF policy type (hard fail, soft fail, neutral, 
absent) and DMARC policy level (p=none, p=quarantine, p=reject, absent).

All domains in these datasets are publicly registered. DNS records are 
public information queryable by anyone. No personal data is included.

## Note on Temporal Validity

DNS records change over time. These datasets represent a snapshot taken 
during Q4 2025 and should be treated as such in any subsequent analysis.
