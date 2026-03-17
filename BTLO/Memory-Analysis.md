# 🧠 Memory Forensics – Ransomware Analysis

## 📌 Overview
This project demonstrates memory forensic analysis on a compromised Windows system using Volatility.  
The objective is to identify malicious processes, determine the initial execution vector, and attribute the infection to a ransomware family.

---

## 🧪 Environment
- OS: Kali Linux  
- Tool: Volatility 3  
- Memory Image: filename.vmem  

---

## 🔍 Analysis Steps

### 1. Process Enumeration (Including Terminated Processes)

vol -f filename.vmem windows.psscan

**Findings:**
- [Suspicious].exe  
- [Ransomware].exe  

---

### 2. Process Investigation via PID

vol -f filename.vmem windows.psscan | grep <PID>

---

### 3. Execution Path Identification

vol -f filename.vmem windows.cmdline

**Result:**
C:\Users\hacker\Desktop\\[Suspicious].exe

---

### 4. Ransomware Identification

[Ransomware].exe → ransomware

---

### 5. Encryption Artifact Discovery (.eky)

vol -f filename.vmem windows.filescan | grep -i ".eky"

---

### 6. Memory Artifact Extraction

vol -f filename.vmem windows.procdump -p <PID>

---

## 🧾 Conclusion

- Suspicious binary executed from user directory  
- Ransomware payload detected  
- Encryption artifacts identified  

➡️ ransomware infection confirmed

---

## 📚 Key Takeaways

- psscan detects hidden processes  
- Memory forensics reveals non-disk artifacts  
- Execution path is key to identifying initial compromise
