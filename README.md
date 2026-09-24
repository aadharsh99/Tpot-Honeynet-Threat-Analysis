# Network Security CA1-T-Pot Honeynet Threat Analysis

A cybersecurity honeynet research project analysing one month of Internet attack activity captured by **T-Pot**, with a focus on the **Cowrie SSH honeypot** and **Honeytrap** low-interaction honeypot.

> **Project type:** Cybersecurity / Honeypot Research / Threat Intelligence / Security Analytics  
> **Primary platform:** T-Pot  
> **Deployment:** DigitalOcean  
> **Observation period:** One month  
> **Analysis focus:** Attack volume, source geography, target ports, source IPs, ASNs, OSINT enrichment, SSH interaction, reconnaissance, and malware downloads.

## Overview

This repository organises the analysis presented in the accompanying NET SEC CA1 report. The study examines real Internet attack telemetry collected by a T-Pot honeynet and uses the data to investigate how automated scanning and intrusion activity appears across different honeypot sensors.

The report identifies two complementary views of attacker behaviour:

- **Honeytrap** — captures early-stage TCP/UDP connection and scanning activity.
- **Cowrie** — captures interactive SSH activity, including command execution and downloaded payloads.

The submitted report states that the month-long deployment produced **around 4 million attack events** across ten active services. Honeytrap and Cowrie accounted for the largest volumes, at just under one million events each.

## Research Objectives

The project investigates:

1. What general attack vectors were observed?
2. Where did the observed attack traffic originate?
3. Which services and ports were targeted?
4. Which source IP addresses generated the highest activity?
5. Which autonomous systems were associated with the activity?
6. What additional intelligence could be obtained through OSINT enrichment?
7. What post-authentication behaviour was visible through Cowrie?
8. How did Honeytrap and Cowrie complement each other in the attack lifecycle?

## Key Findings

### Overall T-Pot activity

The report describes approximately **4 million attack events** across ten active services during the month-long deployment.

The highest-volume sensors included:

| Sensor | Approx. activity described in report |
|---|---:|
| Honeytrap | ~1 million |
| Cowrie | ~1 million |
| Sentrypeer | ~560k |
| Dionaea | ~410k |
| Ciscoasa | ~154k |
| Heralding | ~81k |
| Mallory | ~21k |
| Tanner | ~20k |
| m0n0wall | ~13k |
| Redishoneypot | ~12k |

The report interprets the high Cowrie/Honeytrap volumes as evidence of substantial automated credential-stuffing, scanning and probing activity.

### Geographic distribution

The report's geographic analysis identifies Brazil as the largest source country in the analysed dataset, followed by the United States, the Netherlands, Seychelles and China. The report also discusses Germany, Singapore, Russia, Hong Kong and Indonesia.

**Important:** country attribution in honeypot data indicates the apparent geolocation of observed source infrastructure; it does not establish the physical identity or location of the human operator.

### Target ports

The report identifies the following prominent destination ports:

- **443/HTTPS — ~70.9%**
- **445/SMB — ~7.8%**
- **5000 — ~6.4%**
- Smaller shares were observed for 22/SSH, 5060/SIP and 80/HTTP.

The report associates this pattern with automated discovery of exposed web services, SMB services and other remotely accessible services.

### High-volume source infrastructure

The report highlights these high-volume source IPs:

- `77.83.240.70`
- `204.76.203.28`
- `45.134.26.47`

It reports that each generated more than 380,000 connection attempts during the observation period and appeared across multiple T-Pot sensors.

WHOIS/registration analysis in the report links the address ranges to RIPE NCC allocations and discusses the likelihood that hosting/VPS infrastructure was involved. This should be treated as infrastructure attribution rather than attribution of the underlying human attacker.

### Cowrie findings

Cowrie exposed activity beyond simple authentication attempts.

The report documents:

- High-volume SSH connection attempts.
- Major attacker ASNs including DigitalOcean-ASN (AS14061), China Unicom (AS4837) and Microsoft Corporation (AS8075).
- Repeated downloads of `redtail` payload variants across multiple CPU architectures.
- Command execution after SSH interaction.
- Reconnaissance commands such as:
  - `uname -s -v -n -r -m`
  - `uname -s -v -n -m 2> /dev/null`
- Encoded command execution, including the example `echo -e "\x6F\x6B"`.

The report interprets these behaviours as consistent with automated SSH intrusion and post-authentication reconnaissance.

### Honeytrap findings

Honeytrap primarily exposed the scanning/reconnaissance stage.

The report describes:

- Repeated TCP/UDP connection attempts.
- Small payloads, approximately 20–60 bytes in selected examples.
- Activity targeting ports such as 8728, 57366 and 8888.
- High-volume infrastructure associated with hosting/cloud providers.
- Prominent ASNs including CHEAPY-HOST (AS401120), Alysycon B.V. (AS49870) and DigitalOcean (AS14061).

The report uses Honeytrap and Cowrie together to illustrate a progression from **initial scanning → service interaction → command execution / payload download**.

## OSINT Enrichment

A SpiderFoot scan was used to enrich selected attacker IP/domain indicators.

The report records:

- 120 total elements.
- 97 distinct entities.
- 5 findings marked high severity.
- No errors.
- 26% open TCP ports.
- 15% associated affiliate IP addresses.
- 12% raw findings from public registries/APIs.

The repository includes the extracted project figures so the analysis can be reviewed alongside the written findings.

## Repository Structure

```text
tpot-honeynet-threat-analysis/
├── README.md
├── .gitignore
├── LICENSE
├── docs/
│   ├── methodology.md
│   ├── findings.md
│   ├── cowrie-analysis.md
│   ├── honeytrap-analysis.md
│   └── attack-lifecycle.md
├── figures/
│   ├── figure-01.*
│   ├── figure-02.*
│   └── ...
├── references/
│   └── references.md
└── data/
    └── README.md
```

## Methodology

The analysis is based on the month-long T-Pot deployment described in the submitted report.

The workflow was:

```text
Internet Attack Traffic
          │
          ▼
     T-Pot Honeynet
          │
   ┌──────┴───────┐
   ▼              ▼
Honeytrap       Cowrie
   │              │
Scanning       SSH interaction
   │              │
   │        Commands / payloads
   └──────┬───────┘
          ▼
    T-Pot / Elastic
      analytics
          │
          ▼
 Source IP / ASN / Geo analysis
          │
          ▼
      SpiderFoot
       OSINT enrichment
          │
          ▼
   Threat behaviour analysis
```

## Data Handling

The original report contains screenshots of dashboards, charts, logs and OSINT results. The repository therefore separates **analysis artefacts** from raw telemetry.

No raw T-Pot database, Elasticsearch index, Cowrie event archive or Honeytrap dataset was supplied with the report. The repository does **not** fabricate or reconstruct missing raw data.

If the original telemetry is later made available, it can be added under `data/` with an accompanying data dictionary and collection-period documentation.

## Security & Ethics

This project analyses unsolicited traffic received by a honeynet. It should be treated as defensive security research.

When publishing honeypot data:

- Avoid publishing credentials or secrets.
- Avoid publishing unnecessary personally identifiable information.
- Treat IP addresses as indicators of observed infrastructure, not proof of human identity.
- Do not interact with attacker infrastructure unless explicitly authorised.
- Preserve the original collection context and timestamps when sharing raw data.
- Use isolated infrastructure for honeypot deployments.

## References

The report's bibliography is reproduced in [`references/references.md`](references/references.md).

## Author

**Aadharsh Anbuchezhian**  
Cybersecurity Graduate  
Dublin, Ireland

