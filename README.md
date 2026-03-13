# Project-5-SSH-Brute-Force-Attack-Detection-with-Wazuh-SIEM

## Project Objective
This project demonstrates how to detect and respond to Unauthorized Access attempts. By monitoring SSH authentication logs, I configured Wazuh SIEM to identify automated "Brute Force" attacks where an attacker tries multiple password combinations to gain entry to a Linux server.

## Lab Architechture
Endpoint: Ubuntu Virtual Machine (Target Server).
SIEM: Wazuh Manager & Dashboard (All-in-one installation).
Log Source: /var/log/auth.log (Linux Authentication logs).
Protocol: SSH (Port 22).

## Attack Simulation
To simulate a real-world brute-force scenario, I performed multiple failed login attempts using a non-existent user.
Attack Tool: SSH (Loopback).
Command: ssh fakeuser@localhost
Process: Attempted login 3+ times with incorrect passwords until the system denied further attempts.

## Detection using Wazuh
Wazuh’s security engine analyzed the logs in real-time. When the threshold for failed logins was met, it triggered a high-severity alert.
Wazuh Rule ID: 2502
Rule Level: 10 (High Severity)
Rule Description: syslog: User missed the password more than one time

## Investigation (SOC Analyst Workflow)
As an analyst, I investigated the "Full Log" provided by Wazuh.
Findings: The logs confirmed the source IP and the target user was fakeuser.
Evidence: Cross-referenced the SIEM alert with the raw system logs using sudo tail -n 20 /var/log/auth.log.

## MITRE ATT&CK Mapping
Tactic             Technique                   ID 
Credential Access  Brute Force                 T1110
Discovery          Network Service Scanning    T1046

## Skills Learned
Log Analysis: Navigating and interpreting Linux /var/log/auth.log.
SIEM Configuration: Filtering and analyzing specific Rule IDs in Wazuh.
Threat Identification: Recognizing the pattern of automated brute force vs. a single failed login.
Troubleshooting: Maintaining service health (Suricata) during security monitoring.

## Final Conclusion
This project successfully proves that Wazuh can effectively monitor and alert on suspicious authentication patterns. By detecting these attempts early, a SOC analyst can implement "Active Response" to block the attacking IP, preventing a full system compromise.
