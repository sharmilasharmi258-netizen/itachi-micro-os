# Itachi Micro-OS: Rust Systems Engineering & Live-Bootable OS
**Course:** Operating Systems | Continuous Assessment 6 (15 Marks)
**Project Lead:** Shreyas & Team

---

## 1. Project Overview

This repository houses the complete engineering deliverable for the **CA-6 Operating Systems Engineering Project**, fulfilling:
1. **The Official CA-6 Coursework:** An educational **10-Layer Micro-OS Kernel implemented in Rust**, featuring boot diagnostics, Task Control Blocks (TCBs), FIFO Ready Queue, preemptive Round Robin CPU scheduler, timer interrupts, spinlock mutual exclusion, bump and page frame memory allocators, and system call transitions.
2. **The Live-Boot USB Hardware Requirements:** A bootable Debian-based Live OS for physical laptop demonstration, featuring out-of-the-box Wi-Fi/LAN hardware compatibility, in-built APT/Aptitude package manager, Snap Store, custom **Itachi Uchiha boot splash logo**, and an empirical boot-time benchmark table.

---

## 2. Repository Layout (Section 22 Standard)

```text
micro-os/
├── Cargo.toml                              # Rust build configuration
├── README.md                               # Root project documentation
├── assets/
│   ├── logo.webp                           # Original Itachi Uchiha motif
│   ├── logo.png                            # High-resolution converted splash image
│   └── logo_ansi.txt                       # 24-bit ANSI color terminal banner
├── docs/
│   ├── architecture.md                     # Layered architecture & Mermaid data flow
│   ├── design.md                           # Rust design decisions & unsafe invariants
│   ├── testing.md                          # Systematic testing plan (TC1 - TC6)
│   └── viva_preparation.md                # Model answers to all 20 Viva questions
├── live_usb/
│   ├── LIVE_BOOT_GUIDE.md                  # Foolproof guide to flash & boot pendrive
│   ├── create_live_usb.sh                  # Shell script to configure Plymouth, APT & Snap
│   ├── boot_analysis/
│   │   └── boot_time_comparison.md         # Component-by-component boot latency data
│   └── plymouth_theme/
│       ├── itachi-splash.plymouth          # Plymouth boot splash theme definition
│       ├── itachi-splash.script            # Display centering & status script
│       └── itachi_logo.png                 # Boot splash logo asset
├── src/
│   ├── main.rs                             # Kernel CLI & Layer 10 demonstration
│   ├── lib.rs                              # Kernel library module exports
│   ├── kernel/
│   │   ├── mod.rs                          # Layer 1 Boot & Layer 2 Diagnostics
│   │   └── syscall.rs                      # Layer 9 System Interface / Syscalls
│   ├── task/
│   │   └── mod.rs                          # Layer 3 Task Control Block (TCB)
│   ├── scheduler/
│   │   └── mod.rs                          # Layers 4 & 5 Ready Queue & Round Robin
│   ├── timer/
│   │   └── mod.rs                          # Layer 6 Hardware Clock & Tick Counter
│   ├── sync/
│   │   └── mod.rs                          # Layer 7 Atomic Spinlock & Critical Sections
│   ├── memory/
│   │   └── mod.rs                          # Layer 8 Bump & Page Frame Allocators
│   └── drivers/
│       └── mod.rs                          # Terminal & VGA ANSI Console Driver
├── tests/
│   └── integration_tests.rs                # Rust integration test suite
├── scripts/
│   └── parse_traces.py                     # Python Gantt chart & Fairness trace parser
├── traces/
│   ├── scheduler_trace.log                 # Human-readable kernel execution log
│   └── scheduler_trace.csv                 # Machine-readable context switch records
└── results/
    └── evaluation_report.md                # Auto-generated performance evaluation
```

---

## 3. Quick Start: Rust Micro-OS Kernel

### Prerequisites
- Rust stable toolchain (`rustc`, `cargo` 1.75+)
- Python 3.8+ (for trace visualization)

### 1. Build the Kernel
```bash
cargo build --release
```

### 2. Run the Layer 10 Integrated Demonstration
```bash
cargo run --release -- --demo
```

### 3. Run the CA-6 Validation Test Suite (TC1 to TC6)
```bash
cargo run --release -- --all-tests
```
Or run individual test cases:
```bash
cargo run --release -- --tc 1    # TC1: Minimum Configuration (2 Tasks)
cargo run --release -- --tc 3    # TC3: Boundary Case (Quantum = 1 Tick)
cargo run --release -- --tc 5    # TC5: Failure Case (OOM & Double-Free)
```

### 4. Run Standard Rust Unit/Integration Tests
```bash
cargo test
```

### 5. Parse Traces & Generate Performance Metrics
```bash
python scripts/parse_traces.py traces/scheduler_trace.csv
```
This generates an ASCII Gantt chart, computes Jain's Fairness Index, and outputs `results/evaluation_report.md`.

---

## 4. Live Pendrive Boot Demonstration (In Front of Sir)

1. **Custom Boot Logo:** Itachi Uchiha red moon graphic displays during boot with custom theme.
2. **WiFi & LAN:** Connect via `nmcli dev wifi connect "Network" password "pass"`.
3. **APT & Aptitude:** Demonstrate `aptitude --version` and `apt --version`.
4. **Snap Store:** Demonstrate `snap --version` and `snap list`.
5. **Boot Latency Data:** Verify with `systemd-analyze blame`.
6. **Rust Kernel:** Run `./target/release/micro_os --demo` directly in the terminal!

---

## 5. Academic Assessment & Viva Defence

Review `docs/viva_preparation.md` for full model answers to all 20 individual viva defence questions specified in Section 32 of CA-6.
