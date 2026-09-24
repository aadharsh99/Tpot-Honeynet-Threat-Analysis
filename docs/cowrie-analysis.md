# Cowrie Analysis

## Role

Cowrie is analysed as the higher-interaction SSH component of the T-Pot deployment.

## Source IPs

The report's Figure 9 lists these top Cowrie source IPs:

| Source IP | Count |
|---|---:|
| 85.142.89.168 | 61,958 |
| 72.146.232.13 | 42,910 |
| 223.27.52.31 | 24,944 |
| 196.251.88.103 | 24,660 |
| 194.50.16.73 | 9,465 |
| 134.209.158.3 | 7,923 |
| 196.251.72.53 | 5,648 |
| 142.171.83.19 | 5,148 |
| 157.230.249.150 | 4,277 |
| 157.245.73.85 | 3,905 |

## ASNs

The report's Figure 10 identifies DigitalOcean-ASN (AS14061) as the largest listed source ASN, followed by China Unicom (AS4837) and Microsoft Corporation (AS8075).

## Malware downloads

The report describes repeated downloads of Redtail variants:

- `redtail.arm7`
- `redtail.arm8`
- `redtail.i686`
- `redtail.x86_64`
- `clean.sh`

The report associates these downloads with IoT botnet activity and DDoS recruitment.

## Command execution

Examples documented in the report include:

```text
echo -e "ok"
uname -s -v -n -r -m
uname -s -v -n -m 2> /dev/null
```

The report interprets these as command-execution testing and system reconnaissance.

## Interpretation

The Cowrie evidence demonstrates that the observed traffic went beyond simple port scanning. Some sessions reached interactive SSH behaviour in which commands were executed and payloads were downloaded.
