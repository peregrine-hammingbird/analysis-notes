# Log Analysis – Compromised WordPress (BTLO)

## Overview
This challenge focused on analyzing web server access logs to identify indicators of compromise within a WordPress environment.

## Objective
- Identify suspicious access patterns
- Determine potential attack vectors
- Extract attacker-related indicators from logs

---

## Initial Assessment
- High volume of HTTP requests observed
- Mixture of normal browser traffic and automated activity
- Indicators of targeted interaction with WordPress-specific endpoints

---

## Analytical Approach

### 1. Traffic Profiling
- Grouped requests by IP address and frequency
- Identified anomalous request patterns compared to baseline traffic

### 2. Endpoint Analysis
- Focused on sensitive WordPress paths (authentication and plugin-related endpoints)
- Looked for repeated or abnormal access attempts

### 3. User-Agent Inspection
- Compared common browser signatures with programmatic clients
- Flagged non-standard or automation-related User-Agents

### 4. Behavioral Correlation
- Correlated request patterns, methods (e.g., POST), and response codes
- Identified sequences consistent with exploitation attempts

### 5. Vulnerability Contextualization
- Mapped observed behavior to known vulnerability patterns
- Used external references (e.g., CVE intelligence) to understand exploitation context

---

## Key Findings
- Suspicious automated activity targeting WordPress functionality
- Evidence of interaction with plugin-related components
- Indicators consistent with exploitation of a known vulnerable component

---

## Analyst Notes
- File paths and endpoints can reveal targeted components even without explicit version information
- User-Agent analysis is useful but should not be solely relied upon
- Combining behavioral patterns with vulnerability intelligence provides stronger attribution

---

## Detection Insights
- Monitor repeated POST requests to application-specific endpoints
- Flag abnormal User-Agent patterns (e.g., scripting libraries)
- Correlate high-frequency requests from single sources
- Track access to plugin-related paths for anomaly detection

---

## Takeaways
- Effective log analysis requires correlation across multiple dimensions (IP, endpoint, behavior)
- Attack detection is often based on patterns rather than single indicators
- Understanding common web application structures (e.g., WordPress) is critical for accurate analysis
