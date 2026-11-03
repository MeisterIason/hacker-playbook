# Tool Usage Guide

## Python
- `python3 -m pwntools`
- `python3 -c "import socket; s=socket.socket(); s.connect(('target', 80))"`
- Custom payload generators

## Bash
- `nmap -sS -p- <target>`
- `hydra -l admin -P list.txt <target> rdp`
- `ffuf -u http://target/FUZZ -w wordlist.txt`

## PowerShell
- `Invoke-WebRequest -Uri http://target -Method Post -Body @{}.`
- `Invoke-CredDump`
- Evasion techniques: encoded commands, AMSI bypass