# Methodology

## Deployment

The project report describes a T-Pot honeynet deployed through DigitalOcean for at least one month. The purpose was to collect real Internet attack traffic and analyse attack vectors, source infrastructure and targeted services.

## Analysis stages

1. Collect attack events from T-Pot sensors.
2. Compare event volume across honeypot services.
3. Analyse source geography.
4. Analyse destination ports.
5. Identify high-volume source IPs.
6. Enrich selected indicators using WHOIS and SpiderFoot.
7. Examine Cowrie SSH interaction and commands.
8. Examine Honeytrap connection/scanning activity.
9. Compare the two sensors as stages of attacker interaction.

## Important interpretation boundary

The analysis describes observed network infrastructure. Geolocation, ASN ownership and WHOIS records can identify an allocated network or hosting provider, but they do not by themselves identify the person operating the traffic.

## Source

All project-specific methodology and findings in this repository are derived from the submitted NET SEC CA1 report.
