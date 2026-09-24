# Honeytrap Analysis

## Role

Honeytrap is described in the report as a low-interaction honeypot used to observe TCP/UDP connection attempts and early reconnaissance.

## Top source IPs

The report's Figure 16 lists:

| Source IP | Count |
|---|---:|
| 77.83.240.70 | 156,195 |
| 204.76.203.28 | 72,293 |
| 45.134.26.47 | 63,093 |
| 43.129.41.203 | 62,595 |
| 45.95.147.229 | 54,700 |
| 43.135.123.64 | 28,788 |
| 68.183.149.135 | 25,913 |
| 196.251.80.143 | 19,629 |
| 87.120.191.13 | 16,131 |
| 107.170.36.5 | 15,614 |

## ASN observations

The report's Figure 17 lists examples including:

- AS401120 — CHEAPY-HOST
- AS49870 — Alysycon B.V.
- AS51396 — Pfcloud UG
- AS14061 — DigitalOcean-ASN
- AS396982 — Google Cloud
- AS198953 — Proton66 OOO
- AS132203 — Tencent Building
- AS135377 — UCLOUD INFORMATION
- AS401116 — NYBULA
- AS16509 — AMAZON-02

## Ports and behaviour

The report highlights activity involving ports such as 8728, 5900–5905, 2222 and 9922, describing them as associated with remote-access or router-management services.

The report also describes selected Honeytrap payloads as short, approximately 20–60 bytes, and interprets this as consistent with automated probing.

## Interpretation

Honeytrap primarily provides visibility into the early reconnaissance stage, while Cowrie provides evidence of deeper SSH interaction.
