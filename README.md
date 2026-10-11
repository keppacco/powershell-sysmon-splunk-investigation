# PowerShell Investigation with Sysmon and Splunk

A SOC lab project investigating a harmless PowerShell simulation using Windows Sysmon logs collected in Splunk.

## Lab environment

- Windows 11 — Sysmon and Splunk Universal Forwarder
- Ubuntu — Splunk running in Docker
- Kali Linux — HTTP server hosting simulation files
- VirtualBox — private lab network

## Investigation

The simulation executed `whoami.exe` and `hostname.exe` and requested a harmless text file from the lab HTTP server.

I investigated the activity in Splunk by:
- Extracting XML fields with `rex`.
- Reconstructing the event timeline.
- Matching `ProcessGuid` and `ParentProcessGuid` to identify child processes.
- Correlating network activity using the host, PID, and timestamp.
- Investigating missing file creation events.

## Findings

- Confirmed execution of `simulation.ps1` and its child processes.
- Correlated a TCP connection to the lab server with the observed PowerShell PID and timing.
- Identified a Sysmon FileCreate coverage gap.
- The collected logs did not confirm the download of `sample.txt`.

This was a controlled simulation and a manual investigation. No real malware or automated detection alert was used.

## What I learned

- Connecting evidence across events and following a PowerShell investigation in Splunk.
- Configuring Splunk and the Universal Forwarder to collect Sysmon logs.
- Creating and validating regular expressions for field extraction.
- Distinguishing confirmed findings from assumptions and telemetry limitations.

Configuration and query development were supported by documentation and AI assistance.

## Report

[Read the investigation report](powershell-sysmon-splunk-investigation.pdf)
