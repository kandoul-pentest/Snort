# Snort
Snort is a tool  to detect real-time threats, analyse recorded traffic files and identify anomalies.
# 🛡️ Snort IDS/IPS - Comprehensive Guide

This repository provides hands-on exercises and examples for mastering **Snort**, the powerful open-source intrusion detection/prevention system (IDS/IPS). Learn to use Snort in sniffer, logger, IDS/IPS modes, and analyze PCAP files.

![Snort Logo](https://www.snort.org/assets/img/snort_logo.png)

## 📌 Table of Contents
1. [Introduction](#-introduction)
2. [Operation Modes](#-operation-modes)
   - [Sniffer Mode](#-sniffer-mode)
   - [Packet Logger Mode](#-packet-logger-mode)
   - [IDS/IPS Mode](#-idsips-mode)
   - [PCAP Analysis](#-pcap-analysis)
3. [Rule Structure](#-rule-structure)
4. [Essential Commands](#-essential-commands)
5. [Troubleshooting](#-troubleshooting)
6. [Resources](#-resources)

---

## 🚀 Introduction
Snort is a versatile network security tool that provides:
- Real-time traffic analysis
- Protocol analysis
- Content searching/matching
- Detection of various attacks and probes

---

## 🔧 Operation Modes

### 📡 Sniffer Mode
Basic packet sniffing:
```bash
# Basic packet display
sudo snort -v -i eth0

# Show application layer data
sudo snort -d -i eth0

# Show full packet details
sudo snort -de -i eth0
# Store packets in /var/log/snort
sudo snort -l /var/log/snort -i eth0

  ## Binary logging (tcpdump format)
sudo snort -l /var/log/snort -b -i eth0
# Basic IDS mode
sudo snort -c /etc/snort/snort.conf -i eth0

# IPS mode (requires inline operation)
sudo snort -c /etc/snort/snort.conf -Q -i eth0

# Fast alerts
sudo snort -c /etc/snort/snort.conf -A fast -i eth0

# Read PCAP file
sudo snort -r capture.pcap -c /etc/snort/snort.conf

# Display first 100 packets
sudo snort -r capture.pcap -n 100
# Hex dump of packets
sudo snort -r capture.pcap -X

# Example rule to detect HTTP traffic:
alert tcp $EXTERNAL_NET any -> $HOME_NET 80 (msg:"HTTP Request Detected"; flow:to_server,established; content:"GET"; http_method; sid:1000001; rev:1;)
