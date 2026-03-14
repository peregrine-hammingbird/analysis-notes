# Ransomeware Investigation Lab (PCAP Analysis)

## Overview
This challenge focused on investigating a ransomware infection using network traffic analysis.  
The goal was to identify the malware family, analyze the infection behavior, and recover the encrypted file.

---

## Tools Used

- Wireshark
- md5sum
- VirusTotal
- TeslaDecoder

---

## Investigation Process

### 1. PCAP Analysis
The provided PCAP file was analyzed using Wireshark.

Suspicious HTTP traffic was identified, including connections to a suspicious domain.

Indicators discovered:

- Suspicious download activity
- Possible command and control communication
- File transfer related to malware execution

---

### 2. Malware Extraction

Using:

File → Export Objects → HTTP

A suspicious executable was extracted from the PCAP.

---

### 3. Malware Identification

The MD5 hash of the extracted file was calculated:

md5sum filename.exe

The hash was searched in VirusTotal.

Result:  
The malware was identified as **TeslaCrypt ransomware**.

---

### 4. Encrypted File Analysis

A file named:
The hash was searched in VirusTotal.

Result:  
The malware was identified as **TeslaCrypt ransomware**.

---

### 4. Encrypted File Analysis

A file named: Tender.pdf.micro

was identified as an encrypted file created by the ransomware.

The `.micro` extension is associated with TeslaCrypt infections.

---

### 5. Decryption

The encrypted file was successfully recovered using:

**BloodDolly's TeslaDecoder**

Steps:

1. Launch TeslaDecoder
2. Select the encrypted extension (`.micro`)
3. Load the master decryption key
4. Decrypt the file

The original file: Tender.pdf

was successfully restored.

---

## Key Takeaways

This challenge simulated a real ransomware investigation workflow:

- Network traffic analysis
- Malware extraction
- Threat intelligence lookup
- Ransomware family identification
- File recovery

It reinforced practical DFIR skills commonly used by SOC analysts and incident responders.

---

## Skills Practiced

- PCAP analysis
- Malware identification
- Threat intelligence usage
- Ransomware behavior analysis
- File recovery techniques
