# SAE AS6802 Time-Triggered Ethernet (TTEthernet) Technical Architecture

## 1\. Executive Summary & Specification Scope

SAE AS6802 standardizes Time-Triggered Ethernet (TTEthernet), a deterministic, fault-tolerant networking technology that establishes time-triggered communication on top of classic IEEE 802.3 Ethernet. Selected for safety-critical avionics (NASA Orion MPCV, Ariane 6, Boeing Starliner), TTEthernet guarantees microsecond-level synchronization while permitting mixed-criticality data on a single physical medium.

### Key Architectural Concepts:

1. **Three Coexisting Traffic Classes**:  
   - **Time-Triggered (TT)**: Transmitted at predefined microsecond time windows established by an offline schedule. TT traffic experiences zero transmission jitter and bounded deterministic delay, pre-empting lower priority traffic.  
   - **Rate-Constrained (RC)**: Compliant with ARINC 664 Part 7 (AFDX). Transmitted with bounded latency and guaranteed bandwidth without global clock synchronization.  
   - **Best-Effort (BE)**: Standard non-deterministic Ethernet traffic transmitted during idle slots between TT and RC transmissions.  
2. **Protocol Control Frames (PCF) & Clock Synchronization**:  
   - Clock synchronization is coordinated via Protocol Control Frames (PCF) assigned dedicated EtherType `0x891D`.  
   - Synchronization modes:  
     - **Integration (IN)**: Periodic operational clock adjustment.  
     - **ColdStart (CS)** and **ColdStart Acknowledge (CA)**: Cluster startup and resynchronization.  
   - **Transparent Clock (TC)**: Network switches measure and append frame transit residence times in the 8-byte transparent clock field, eliminating switch queuing jitter.  
3. **Fault-Tolerant Clock Synchronization Algorithm**:  
   - Employs a fault-tolerant median algorithm where Compression Masters (switches) evaluate multiple Synchronization Master inputs and broadcast compressed time correction values.  
4. **Safety & Redundancy**:  
   - Dual-channel permanent redundancy (Redundant Network A & B) with independent power and physical routing, certified up to DO-254 / DO-178C DAL-A.