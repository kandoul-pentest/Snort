# Snort
Snort is a tool  to detect real-time threats, analyse recorded traffic files and identify anomalies.



# 🛡️ Snort IDS/IPS - Comprehensive Guide

![Snort Logo](https://www.snort.org/assets/img/snort_logo.png)

Snort is an open-source intrusion detection/prevention system (IDS/IPS) that provides real-time traffic analysis, protocol analysis, content searching/matching, and detection of various attacks and probes.

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
Basic packet sniffing
# Basic packet display
sudo snort -v -i eth0

# Show application layer data
sudo snort -d -i eth0

# Show full packet details
sudo snort -de -i eth0

# Store packets in /var/log/snort
sudo snort -l /var/log/snort -i eth0

# Packet Logger Mode :Binary logging (tcpdump format)
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
alert tcp $EXTERNAL_NET any -> $HOME_NET 80 (
    msg:"HTTP Request Detected";
    flow:to_server,established;
    content:"GET";
    http_method;
    sid:1000001;
    rev:1;
).
