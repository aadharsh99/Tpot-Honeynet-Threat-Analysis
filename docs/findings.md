# Findings

## 1. Overall attack volume

The report describes approximately four million attack events across ten active T-Pot services during the one-month deployment.

Honeytrap and Cowrie recorded the largest volumes, each at approximately one million events.

## 2. Geography

The report identifies Brazil as the largest apparent source country in the analysed dataset, followed by the United States, the Netherlands, Seychelles and China.

The report also identifies Germany, Singapore, Russia, Hong Kong and Indonesia among the other observed source countries.

## 3. Destination ports

The report gives the following approximate distribution:

| Port | Service/context | Share |
|---:|---|---:|
| 443 | HTTPS | 70.9% |
| 445 | SMB | 7.8% |
| 5000 | UPnP/HTTP context in report | 6.4% |
| 22 | SSH | <5% |
| 5060 | SIP | <5% |
| 80 | HTTP | <5% |

These figures are reproduced from the report and should be treated as observations from this particular deployment.

## 4. High-volume source IPs

The report identifies:

- 77.83.240.70
- 204.76.203.28
- 45.134.26.47

Each is described as producing more than 380,000 connection attempts during the observation period.

## 5. Infrastructure

The report repeatedly identifies cloud/hosting infrastructure in its ASN analysis. Cowrie's top ASN examples include DigitalOcean, China Unicom and Microsoft. Honeytrap's examples include CHEAPY-HOST, Alysycon B.V. and DigitalOcean.

## 6. Cowrie post-authentication behaviour

The report documents command execution, reconnaissance and malware downloads. Redtail variants were among the downloaded files and appeared across multiple CPU architectures.

## 7. Honeytrap reconnaissance

Honeytrap recorded repeated TCP/UDP connections and small payloads. The report interprets this as early-stage automated scanning.

## 8. Combined attack lifecycle

The report's central analytical interpretation is that Honeytrap and Cowrie provide complementary visibility:

```text
Reconnaissance
      ↓
Port / service scanning
      ↓
Authentication attempts
      ↓
SSH interaction
      ↓
Command execution
      ↓
Payload download / post-compromise activity
```
