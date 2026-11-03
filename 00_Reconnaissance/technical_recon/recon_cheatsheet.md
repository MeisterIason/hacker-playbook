# Recon Cheatsheet

## Nmap Scan Profiles
```
# Aggressive scan
nmap -A -T4 <target>

# Stealth SYN scan
nmap -sS -T2 <target>

# Service/version detection
nmap -sV <target>

# OS detection
nmap -O <target>
```

## Shodan Queries
```
# Devices with port 22 open
port:22

# Web servers with Apache
product:"Apache"

# Exposed Redis instances
port:6379
```

## Domain Analysis
```
; WHOIS example
whois example.com

; DNS enumeration
dig axfr example.com @ns1.example.com
```