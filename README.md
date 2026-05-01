# 🔌 UART 16550A Controller with AMBA APB Interface

> A fully functional RTL implementation of the industry-standard 16550A UART on a 32-bit APB bus, designed in Verilog HDL with complete functional verification.

---

## 📡 Live Simulation & Waveforms

**👉 [View Simulation & Waveforms on EDA Playground](https://edaplayground.com/x/V3fg)**

Open the link above to run the testbench live in your browser and inspect the simulation waveforms — no tools installation required.

---

## 📖 Overview

This project implements a **UART 16550A controller** with an **AMBA APB (Advanced Peripheral Bus) interface**, enabling efficient and reliable serial communication. The design follows industry-standard 16550A UART specifications and is structured for synthesis and simulation using **Xilinx ISE** and **Intel Quartus Prime**.

---

## ✨ Features

- **AMBA APB Interface** — Standard 32-bit peripheral bus integration
- **Configurable Baud Rate Generator** — Divisor latch for flexible baud rate selection
- **16-byte TX/RX FIFOs** — Reduces CPU intervention and handles burst data
- **Interrupt-Driven Data Handling** — Interrupt enable/status registers for event-driven operation
- **Full 16550A Register Set** — RBR, THR, IER, IIR, FCR, LCR, MCR, LSR, MSR, SCR
- **Line Control** — Configurable data bits, stop bits, and parity
- **Loopback Mode** — Internal diagnostic loopback for self-testing
- **Gate-Level Netlist** — Design validated post-synthesis

---

## 🏗️ Architecture

```
┌──────────────────────────────────────────────────────┐
│                   APB Bus Interface                   │
│          (PSEL, PENABLE, PWRITE, PWDATA, PRDATA)      │
└───────────────────────┬──────────────────────────────┘
                        │
          ┌─────────────▼──────────────┐
          │      Register File          │
          │  (LCR, IER, FCR, MCR, ...)  │
          └──┬──────────────────────┬──┘
             │                      │
    ┌────────▼──────┐     ┌─────────▼──────┐
    │  TX Path       │     │  RX Path        │
    │  ┌──────────┐  │     │  ┌──────────┐  │
    │  │ TX FIFO  │  │     │  │ RX FIFO  │  │
    │  └────┬─────┘  │     │  └────▲─────┘  │
    │  ┌────▼─────┐  │     │  ┌────┴─────┐  │
    │  │TX Shift  │  │     │  │RX Shift  │  │
    │  │ Register │  │     │  │ Register │  │
    │  └────┬─────┘  │     │  └────▲─────┘  │
    └───────│────────┘     └───────│────────┘
            │      ┌───────┐       │
            └─────►│  Baud │◄──────┘
                   │  Gen  │
                   └───────┘
```

---

## 🔧 Register Map (16550A Compatible)

| Offset | Register | Description |
|--------|----------|-------------|
| 0x00 | RBR / THR / DLL | Receive Buffer / Transmit Holding / Divisor LSB |
| 0x04 | IER / DLM | Interrupt Enable / Divisor MSB |
| 0x08 | IIR / FCR | Interrupt ID / FIFO Control |
| 0x0C | LCR | Line Control (data bits, parity, stop bits) |
| 0x10 | MCR | Modem Control |
| 0x14 | LSR | Line Status (TX empty, RX data ready, errors) |
| 0x18 | MSR | Modem Status |

---

## 🧪 Verification

Functional verification was performed using Verilog testbenches covering:

- APB write/read transactions to all registers
- UART transmit and receive data path (loopback)
- Baud rate divisor configuration and validation
- FIFO full/empty boundary conditions
- Interrupt generation for RX data available and TX empty events
- Line status error injection (framing, parity, overrun)

**Post-synthesis gate-level simulation** was also performed to validate timing and netlist correctness.

---

## 🛠️ Tools Used

| Tool | Purpose |
|------|---------|
| Xilinx ISE | RTL design, synthesis, and simulation |
| Intel Quartus Prime | Cross-tool synthesis and validation |
| EDA Playground | Cloud-based simulation and waveform viewing |

---

## 🚀 Getting Started

### Run in Browser (Recommended)

The fastest way to see this design in action:

**[▶ Open on EDA Playground](https://edaplayground.com/x/V3fg)** — click **Run** to simulate and view the waveforms directly in your browser.

---

*Designed and verified in Verilog HDL. Simulations available on [EDA Playground](https://edaplayground.com/x/V3fg).*
