# Communication-Network
## Covert Communication Network on macOS Terminal

### Business & Product Understanding

#### 🔹 Overview
This project provides a covert, secure, and decentralized communication network using Tor, SSH tunneling, steganography, and encryption. The goal is to enable private messaging and file sharing while ensuring infrastructure uptime and security.

#### 🔹 Use Cases
- Secure communication in high-surveillance environments
- Anonymous file sharing via Tor hidden services
- End-to-end encrypted messaging without third-party interference
- Covert data transmission using steganography

--- 

### Features

- ✅ Tor Hidden Service – Anonymous communication channel
- ✅ SSH over Tor – Secure encrypted access
- ✅ Steganography – Hide messages inside images
- ✅ Persistent Infrastructure – Services restart after reboot
- ✅ Encryption – AES-256 encryption for files

--- 

### Installation

1️⃣ Install Dependencies
Run the following command in macOS Terminal:
```bash
brew install tor openssh nmap socat steghide
```
2️⃣ Configure Tor Hidden Service
Edit the Tor configuration file:
```bash
sudo nano /opt/homebrew/etc/tor/torrc
```
Add the following:
```bash
HiddenServiceDir /usr/local/var/lib/tor/hidden_service/
HiddenServicePort 80 127.0.0.1:8080
```
Restart Tor:
```bash
brew services restart tor
```
Retrieve your .onion address:
```bash
cat /usr/local/var/lib/tor/hidden_service/hostname
```

--- 

### Usage

1️⃣ Start a Hidden Web Server
```bash
nohup python3 -m http.server 8080 > /dev/null 2>&1 &
```
Access it via:
```bash
http://yourgenerated.onion
```
2️⃣ Secure SSH Connection Over Tor
```bash
torsocks ssh -i ~/.ssh/covert_key user@yourgenerated.onion
```
3️⃣ Hide & Extract Messages Using Steganography
Embed a Message:
```bash
steghide embed -cf secret_image.jpg -ef message.txt -p "password"
```
Extract the Message:
```bash
steghide extract -sf secret_image.jpg -p "password"
```
4️⃣ Encrypt & Decrypt Files
Encrypt a file:
```bash
gpg --symmetric --cipher-algo AES256 secret.txt
```
Decrypt a file:
```bash
gpg --decrypt secret.txt.gpg
```

--- 

### Security & Maintenance

1️⃣ Disable System Logs
```bash
sudo rm -rf /var/log/*
sudo ln -s /dev/null /var/log/syslog
```
2️⃣ Monitor Anonymity
```bash
netstat -an | grep 9050
nmap -sS -T4 -Pn localhost
```
3️⃣ Automate Persistence
Add services to crontab:
```bash
crontab -e
```
Add:
```bash
@reboot tor
@reboot nohup python3 -m http.server 8080 > /dev/null 2>&1 &
```
--- 

### Conclusion

This project creates a fully covert, decentralized, and secure messaging system using anonymous Tor routing, encryption, and steganography. It is designed to stay online, resist surveillance, and protect user privacy.
