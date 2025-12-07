# 8T-SRAM-CIM
Architecturally eliminating the von Neumann bottleneck using a high-stability 8T SRAM Compute-In-Memory (CIM) macro designed and validated in 90 nm CMOS for high-throughput edge AI.

**Team Members:** Prasanna Kumar, Rishabh TR, Sagar S Ajjaplar, Sampath Sajjan.

## 1. Executive Abstract: Eliminating the Memory Wall

Conventional von Neumann architectures suffer from the critical **"memory wall" bottleneck**, where data transfers consume themajority of system power and severely restrict throughput in data-intensive applications like AI/ML.

This project presents a robust solution using the **8-Transistor (8T) Static Random Access Memory (SRAM)** cell, which is architecturally optimized for Compute-In-Memory (CIM).

We successfully designed and verified the core 8T cell in **90 nm CMOS technology** using Cadence Virtuoso. The decoupled Read/Write architecture **eliminates the destructive read disturbance** problem inherent in standard 6T cells, guaranteeing data integrity.

### Key Breakthroughs: Quantification and Validation
| Metric | Result | Impact |
| :--- | :--- | :--- |
| **Read Stability (RSNM)** | **558.3 mV** | Quantitatively proves immunity to read disturbance, critical for reliable sensing. |
| **Operational Speed (Write Delay)** | **67.0 ps** | Achieves sub-nanosecond write performance, accelerating CIM cycle time. |
| **Statistical Robustness** | **100% Yield** (200 Monte Carlo runs passed) | Validated resilience against manufacturing process variations (PVT) at the 90 nm node. |
| **Baseline Energy** | **3.88 pJ** per cycle | Provides low-power baseline for comparison against final array-level energy reduction. |

***

## 2. Architectural Design and Methodology

### 2.1. The High-Stability 8T SRAM Cell
The selection of the 8T architecture over the conventional 6T was mandated by the need for absolute data integrity during in-memory operations. The 8T cell achieves robustness by decoupling access pathways:

1.  **Storage Core (M1-M4):** A cross-coupled CMOS latch stores the data (Q/QB).
2.  **Write Port (M5, M6):** Controlled by the Write Word Line (WWL), facilitating differential data input via WBL/WBLB.
3.  **Dedicated Read Port (M7, M8):** Controlled by the Read Word Line (RWL). This dedicated path connects node Q to the Read Bit Line (RBL) without disturbing the internal nodes, ensuring a non-destructive read.

### 2.2. CIM Array Implementation
*   **Technology Node:** 90 nm CMOS Process Design Kit (PDK).
*   **Design Toolchain:** Cadence Virtuoso Schematic Editor and Spectre Simulator.
*   **Array Prototype:** An **8x8 array** was constructed, utilizing **asymmetric sense amplifiers** designed for differential sensing of Boolean results.
*   **Realistic Load Modeling:** Simulations rigorously incorporated a realistic bitline model consisting of a **10 kΩ resistor** and a **50 fF capacitor** connected to the RBL, ensuring accurate delay and power calculations under array conditions.

### 2.3. Implemented Compute Functions
The design demonstrates capability for robust parallel processing via **multi-row activation**.

| Function Type | Operations Implemented | Principle of Operation |
| :--- | :--- | :--- |
| **Boolean Logic** | NAND, NOR, AND, OR | Differential sensing scheme utilizing modified sense amplifiers across multiple activated rows. |
| **Arithmetic** | Half-Adder, Half-Subtractor | Implemented by mapping **NOR-based netlists** into the SRAM memory array structure. |

***

## 3. Detailed Verification Metrics

The following metrics were extracted from rigorous DC, Transient, and Monte Carlo simulations (200 runs for statistical data).

### 3.1. Cell Stability Analysis (SNM)
The Static Noise Margin (SNM) quantifies the cell’s resilience against electrical noise.

| Parameter | Mnemonic | Calculated Value | Significance |
| :--- | :--- | :--- | :--- |
| Hold Static Noise Margin | HSNM | **848.5 mV** | Stability in idle state. |
| Read Static Noise Margin | RSNM | **558.3 mV** | Critical stability during read operation. |
| Write Static Noise Margin | WSNM | **446.8 mV** | Write-ability threshold (minimum voltage required to flip the cell). |

### 3.2. Dynamic Performance and Power Efficiency
| Parameter | Calculated Value | Unit | Description |
| :--- | :--- | :--- | :--- |
| **Write Delay** | **67.0** | ps | Time required to successfully write a new value. |
| **Read Delay** | **111** | ps | Time required to discharge the RBL and sense data. |
| Static Power Dissipation | 67.5 | nW | Baseline leakage when the cell is idle. |
| **Energy per Cycle** | **3.88** | pJ | Fundamental metric for energy efficiency (measured in 100ns cycle) |
| Peak Power Draw | 168.8 | µW | Maximum instantaneous power during a switching event |
