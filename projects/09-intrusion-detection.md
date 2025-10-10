---
layout: page
title: CP 330 - Edge AI
subtitle: Indian Institute of Science | January 2025
---

## AI–Based Intrusion Detection System for CAN Bus Security

### Introduction

Modern vehicles and industrial controllers rely on the CAN bus for real–time communication among ECUs. Because CAN has no built-in authentication or encryption, it is vulnerable to spoofing, flooding, and fuzzing attacks. This project demonstrates an edge-AI IDS: an Arduino-based CAN traffic generator simulates benign and malicious frames, while a Raspberry Pi Pico monitors the bus, extracts features in real time, applies a compact Decision Tree model, and raises alerts via USB CDC with sub-millisecond latency.

<!-- **Integration Diagram (placeholder):**  
**Figure 1:** System Integration Diagram -->

- **CAN Vulnerabilities:** No frame integrity or source authentication.  
- **Attack Scenarios:** Denial-of-Service flooding, fuzzing, impersonation.  
- **Existing Defenses:** Hardware firewalls add cost; cloud analytics add latency.  
- **Edge AI Advantage:** Local inference on microcontrollers ensures low latency and resilience.

---

### Methodology

#### About the Setup and Flow

Two physical nodes share a single CAN bus:

- **Attack Node:** Arduino Uno R3 + MCP2515 — generates four traffic modes (Valid CAN sweep, DoS, Fuzzy, Impersonation) and mirrors each frame as Lawicel ASCII over UART.  
- **IDS Node:** Raspberry Pi Pico + MCP2515 — listens in parallel, timestamps and parses UART frames, extracts features, classifies each frame, and logs alerts over USB CDC.

**Flow Diagram (placeholder):**  
**Figure 2:** Data Flow Between Nodes

#### About the MCP2515

The MCP2515 is a stand‑alone CAN controller interfacing via SPI to microcontrollers. Key specifications:

- 8 MHz crystal, up to 1 Mbps CAN speed  
- Two 8-byte RX FIFOs and three TX buffers  
- Six message acceptance filters with masking  
- INT pin indicates RX/TX events  
- Requires 120 Ω termination on CAN H and CAN L
<!-- 
## 3.3 Selection of Models and Testing Accuracy

*(Summary in section 3.4 and Table 1 below.)* -->

#### Attack Node and Victim Node

**Attack Node Modes:**

- **Valid CAN Data (Score 0):** benign sweep of known IDs at 10 fps  
- **DoS Attack (Score 1):** ID `0x000` at 3 kfps  
- **Fuzzy Attack (Score 2):** random ID and payload at 3 kfps  
- **Impersonation (Score 3):** ID `0x105` with fixed malicious payload

**Model performance (comparison of tree-based classifiers):**

| Model         | Accuracy | Precision | Recall |
|---------------|---------:|----------:|-------:|
| Decision Tree | 83.5 %   | 84.2 %    | 85.0 % |
| Random Forest | 89.2 %   | 90.1 %    | 91.3 % |
| XGBoost       | 91.0 %   | 92.0 %    | 92.5 % |

**Table 1:** Comparison of tree-based classifiers.

Decision Tree was selected for its minimal code size (~30 kB) with acceptable accuracy.

- **Victim Node:** Captures mirrored UART frames, extracts 19 features, applies Decision Tree inference, and prints scores/alerts in real time.

<!-- ## 3.5 Integration Diagram

**Figure 3:** Detailed Hardware Integration -->

### Data Collection

We collected a total of **5.4 million CAN frames** in four categories:

- **Attack free (Valid, Score 0):** 800k frames each for three runs (2.4M total)  
- **DoS Attack (Score 1):** 1M frames on ID `0x000`  
- **Fuzzy Attack (Score 2):** 1M frames with random IDs/payloads  
- **Impersonation (Score 3):** 1M frames on ID `0x105`

Each log entry used the format:

Timestamp: 0.123456 ID: 080 000 DLC: 8 AA BB CC ... FF


### Feature Explanation and Importance

We extract 19 features per frame. Together they capture payload content, timing, and structural anomalies:

1. **CAN ID:** Numeric identifier; unexpected IDs signal spoofing/impersonation.  
2. **DLC (Data Length Code):** Byte count; abnormal DLC patterns indicate malformed frames.  
3. **Byte 0 ... Byte 7:** Each raw payload byte; basis for content analysis.  
4. **Payload Sum:** Sum of 8 bytes; sudden jumps reveal bulk data changes (fuzzing).  
5. **Payload Mean:** Average byte value; detects systematic zero fills (DoS).  
6. **Payload Std:** Standard deviation; low for static payloads, high for random fuzzed data.  
7. **Entropy:** Shannon entropy of byte distribution; high for random data, low for repetitive patterns.  
8. **Timestamp Diff:** Time since last same-ID frame; short intervals indicate flooding.  
9. **MessageFrequency:** Cumulative count per ID; rapid growth flags high-rate attacks.  
10. **InterArrival:** Difference of successive Timestamp Diff; measures burstiness and irregular timing.  
11. **DLC Variability:** Rolling std. dev. of DLC; fluctuating DLC suggests fuzzing.  
12. **ErrorFrame:** Flag if DLC == 0; error frames may arise from collisions or intentional faults.  
13. **RollingWindowRate:** Frames per second in sliding window; sustained high rates → DoS.  
14. **PayloadRepetitionCount:** Count of identical payloads per ID; replay attacks manifest here.  
15. **ByteCorrelation:** Correlation between bytes across recent frames; structural payload changes trigger anomalies.  
16. **EntropyTrend:** Change in entropy over window; sudden increases indicate fuzzing onset.  
17. **TimestampDrift:** Deviation from expected inter-frame gap; bus congestion or tampering effects.  
18. **FrameSizeRatio:** DLC/8 ratio; abnormal small or full-size patterns suggest malicious framing.  
19. **WhitelistFlag:** Binary indicator if ID is in known safe list; unknown IDs treated as impersonation candidates.

### Model Development and Compression

1. Built a dataset with **5.4M samples × 19 features**.  
2. Stratified **80/20** train/test split.  
3. Trained a Decision Tree (max depth = 6).  
4. Obtained **Accuracy 83.5 %**, **Precision 84.2 %**, **Recall 85.0 %**.  
5. Exported via `m2cgen` to C code (`model.c`/`model.h`), size ~30 kB.

### Deployment

The Pico firmware (`main.c`) implements:

- Robust S-LCAN parsing (3–4 digit IDs, padded payloads).  
- Inline feature extraction and `score(feat)` invocation.  
- USB CDC output via `printf()`.

<!-- **Build & Flash:**
```bash
mkdir build && cd build
cmake .. && make -j4
# Drag-and-drop pico_can_rf_model.uf2 onto the Pico -->

### Prototype and Demonstration

Live console example:

`[RX] t0008AABBCCDDEEFF`

`Score 0`

`[RX] t0008AABBCCDDEEFF`

`Score 1`

### Challenges and Workarounds

- **MCP2515 failure** → Arduino-only loopback with simulated latency.  
- **UART conflict** → moved Pico UART to `SoftwareSerial` on D8/D9.  
- **USB enumeration delay** → added `sleep_ms(1500)` and enabled CDC in CMake.


### Project Resources

- **Code repository:** https://github.com/Manoj-prog-use/EdgeAI_CANIDS/tree/main  
- **Arduino sketch:** `attack_modes.ino`  
- **Pico firmware:** `main.c`, `model.c`, `CMakeLists.txt`  
- **Training notebook:** `CAN_IDS_DF.ipynb`