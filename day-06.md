# Day 06 — Nmap & Reconnaissance

## 1. Open Port vs Closed Port

- **Open Port:** A port is open when a service is listening and accepting connections.
- **Closed Port:** A port is closed when the host is reachable, but no service is listening on that port.

## 2. Nmap Scan — scanme.nmap.org

**Command:**

```bash
nmap -oN ~/lab/notes/scan1.txt scanme.nmap.org
```

**Scan Results:**

- Domain: `scanme.nmap.org`
- IP Address: `45.33.32.156`
- Host Status: Up
- Open Ports: 3
- Closed Ports: 997

| Port | State | Service |
|---|---|---|
| 22/tcp | Open | SSH |
| 80/tcp | Open | HTTP |
| 9929/tcp | Open | nping-echo |

**Result file:** `~/lab/notes/scan1.txt`

## 3. Local Server — Port 8000

### Server ON

**Command to start the server:**

```bash
python3 -m http.server 8000 --bind 127.0.0.1
```

**Scan result:**

```text
8000/tcp open http-alt
```

The local server was running and accepting connections on port 8000.

### Server OFF

When the local server was stopped, the scan showed no open ports in the tested range.

**Observed result:**

```text
Host: 127.0.0.1 (localhost)
Ports: Ignored State: closed (10000)
```

## 4. TCP Connect Scan vs TCP SYN Scan

- **TCP Connect Scan (`-sT`):** Completes the TCP three-way handshake.
- **TCP SYN Scan (`-sS`):** Does not complete the three-way handshake; it sends a reset after receiving a SYN/ACK response from an open port.

## 5. Passive Recon vs Active Recon

- **Passive Recon:** Collects information from public sources without directly interacting with the target.
- **Active Recon:** Interacts directly with the target system or its people to gather information.

## 6. Practical Files

| File | Purpose |
|---|---|
| `scan1.txt` | Saved Nmap scan of scanme.nmap.org |
| `local.gnmap` | Saved local port scan result |
| `scan_local.sh` | Bash script to check local open ports |

**Script location:** `~/lab/scripts/scan_local.sh`

**Script content:**

```bash
#!/bin/bash
echo "Local open ports:"
nmap -p 1-10000 -oG - 127.0.0.1 | grep "Ports:"
```

## 7. Passive Recon — WHOIS and DNS

Attempted commands:

```bash
dig @1.1.1.1 tryhackme.com A +short
whois tryhackme.com
```

**Result:** The AttackBox could not reach the external DNS/WHOIS servers.

Error:

```text
Network is unreachable
```

The WHOIS registrar and name server information could not be verified, so no unconfirmed results are recorded.

## 8. Day 06 Summary

- Practised Nmap port scanning.
- Identified open and closed ports.
- Performed TCP Connect, TCP SYN and UDP scans in the TryHackMe lab.
- Tested a local HTTP server on port 8000.
- Created a Bash script for local port scanning.
- Learned the difference between passive and active reconnaissance.
- Attempted WHOIS and DNS reconnaissance.

- ## 9. Practical Screenshots / Proof

![Nmap Scan](./screenshots/nmap-scanme.png)

![Local Server ON](./screenshots/local-server-on.png)

![Local Server OFF](./screenshots/local-server-off.png)
