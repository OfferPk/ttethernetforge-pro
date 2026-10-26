# TTEthernetForge Pro User Guide & Developer Manual

## 1\. Quickstart Guide

1. Launch `index.html` in your web browser.  
2. In the "TTEthernet Node & Schedule Config" panel, set your Synchronization Domain ID (e.g. `1`).  
3. Select the Node Synchronization Role (`Synchronization Master SM`, `Compression Master CM`, or `Synchronization Client SC`).  
4. Select Protocol Control Frame (PCF) Type (`Integration Frame IN` or `ColdStart Frame CS`).  
5. Choose the Traffic Class schedule slot (`Time-Triggered TT`, `Rate-Constrained RC`, or `Best-Effort BE`).  
6. Click **Transmit PCF Sync Frame** to generate the 60-byte Ethernet frame with EtherType `0x891D`, compute transparent clock transit delays, and inspect the binary PCF dissector.  
7. Click **Verify Traffic Slot** to evaluate latency and jitter bounds across the schedule.  
8. Click **Run Normative Audit** to evaluate all 10 SAE AS6802 protocol compliance checks.

## 2\. Standalone Headless Python CLI

Run automated regression testing and compliance verification:

python3 tteth-cli.py \--audit \--domain 1 \--role SM