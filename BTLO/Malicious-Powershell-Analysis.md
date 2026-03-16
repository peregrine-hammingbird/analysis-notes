# Malicious PowerShell Analysis – Threat Investigation

## Overview
This investigation focused on analyzing an obfuscated PowerShell command commonly used in malware delivery.

The script used Base64 encoding, string obfuscation, and Windows native tools to download and execute a malicious payload.

## Initial Observation

The suspicious command used the following parameters:

PowerShell -w hidden -ENCODEDCommand

Key indicators:
- `-w hidden` (hidden window execution)
- `-EncodedCommand` (Base64 encoded PowerShell script)

This technique is commonly used by attackers to evade detection.

---

## Step 1 – Decoding the PowerShell Command

The encoded command was Base64 encoded using **UTF-16LE**, which is the default encoding for PowerShell `EncodedCommand`.

### Decoding Process

Tool used:

CyberChef

Recipe:

From Base64  
Decode Text (UTF-16LE)

After decoding, the script revealed heavily obfuscated PowerShell code using:

- string concatenation (`'a'+'b'`)
- format operator (`-f`)
- variable indirection

---

## Step 2 – Script Deobfuscation

The script reconstructed strings dynamically using concatenation.
Which resolves to: [Answer]

The script also dynamically referenced .NET classes.

Example:

[Net.ServicePointManager]::SecurityProtocol = ""

This forces [Answer] for outbound network communication.

---

## Step 3 – Directory Creation

The malware constructs a directory path using PowerShell variables and format operators.

Purpose:
- store downloaded payload
- evade casual user detection

---

## Step 4 – Payload Download

The script attempts to download a malicious DLL from several compromised domains.

Observed behavior:

System.Net.WebClient.DownloadFile()

The downloaded file is saved as:

[Answer]

---

## Step 5 – Payload Execution

Execution is performed using a Windows built-in utility.

Tool used:

[Answer].exe

Example execution pattern:

[Answer].exe ,[Answer]<exported function>

This is a common **Living-off-the-Land (LOLbins)** technique used to execute malicious DLL payloads while blending with legitimate system processes.

---

## Step 6 – Network Indicators

The script contained multiple domains used as fallback download sources.

Example indicator:

[Answer]/content/6F2gd/

These domains are used as potential payload delivery infrastructure.

---

## Key Techniques Observed

- PowerShell encoded command execution
- Base64 + UTF-16LE encoding
- string concatenation obfuscation
- dynamic variable resolution
- WebClient payload download
- rundll32 execution
- LOLbins abuse
- multi-domain fallback infrastructure

---

## Security Implications

This script behaves as a **malware downloader** designed to:

1. evade detection using PowerShell obfuscation
2. download a second-stage payload
3. execute it using native Windows utilities

Such techniques are frequently observed in modern malware campaigns.

---

## Skills Practiced

- PowerShell malware analysis
- script deobfuscation
- threat hunting techniques
- malicious infrastructure identification
- DFIR investigation workflow

---

## Tools Used

- CyberChef
- manual PowerShell analysis
- threat investigation techniques
Example technique used by the malware:('T' + ('ls' + '12'))

