# FoundationForge Pro (v1.0.0)

**FOUNDATION Fieldbus H1 (IEC 61158-2 / ISA-50.02) Protocol Studio, Link Active Scheduler (LAS) Macrocycle Engine, Physical Segment Voltage Drop Sizer, & 10-Point Safety Auditor**

---

## ⚡ Overview

**FoundationForge Pro** is an industrial process automation engineering suite specifically targeted at **FOUNDATION Fieldbus H1 (IEC 61158-2 / ISA-50.02 / FF-890)** continuous process networks (refineries, petrochemical plants, offshore platforms, power plants). It delivers zero-dependency, browser-based, and command-line automation for:

1. **Manchester Biphase-L Physical Frame Engine**: Models 31.25 kbps MBP signaling, 0xAC Start Delimiter, 0xAD End Delimiter, and CRC-16 Frame Check Sequences (\$x^{16} \+ x^{12} \+ x^5 \+ 1\$).  
2. **5-Byte Process Value (PV) Quality Engine**: Packs and unpacks 4-byte IEEE-754 floating-point process values alongside the 1-byte Fieldbus Status byte (Quality: Good, Uncertain, Bad; Limits: High, Low, Constant).  
3. **Link Active Scheduler (LAS) Macrocycle Engine**: Automatically schedules deterministic cyclic communication (Time Distribution, Compelled Data publish broadcasts for AI \$\\rightarrow\$ PID \$\\rightarrow\$ AO) and preserves balanced acyclic Pass Token (PT) windows (\$\\ge 30%\$) for diagnostic traffic.  
4. **Physical Segment Voltage Drop & Spur Sizer**: Models Type A cable loop resistance (\$44\\ \\Omega/\\text{km}\$), 24V DC power conditioner drops, and individual/cumulative spur constraints to ensure \$\\ge 9.0\\text{V DC}\$ terminal voltage at distant field transmitters.  
5. **10-Point FF H1 Physical & LAS Safety Auditor**: Verifies permanent address ranges (`0x10..0xF7`), address collisions, 32-device limits, 1900m Type A cable budgets, dual 100-ohm RC bus terminators, and Backup Link Master (LM) redundancy.  
6. **DCS Exporter**: Generates Emerson DeltaV / AMS Fieldbus Segment XML definitions, Yokogawa CENTUM VP schedule CSVs, and Python 31.25 kbps virtual bus scripts.

---

## 📁 Repository Structure

product\_197/

├── source-code/

│   ├── fieldbus-engine.js           \# Manchester framing, delimiters, CRC-16, PV packing

│   ├── fieldbus-scheduler.js        \# LAS Macrocycle scheduling & CIF loop sequencing

│   ├── fieldbus-segment-sizer.js    \# Type A/B/C cable resistance & voltage drop math

│   ├── fieldbus-auditor.js          \# 10-Point FF H1 physical & LAS safety auditor

│   ├── fieldbus-forge.css           \# Process safety dark amber/orange UI theme

│   ├── app.js                       \# Interactive web controller

│   └── index.html                   \# Responsive 5-tab web studio

├── build/

│   ├── fieldbus-cli.py              \# Standalone Python CLI executable (chmod \+x)

│   └── foundationforge-pro-v1.0.0.zip\# Production release archive

├── documentation/

│   ├── ARCHITECTURE.md              \# Engineering specification & protocol mathematics

│   ├── USER\_GUIDE.md                \# Operator manual & CLI instructions

│   ├── MONETIZATION\_AND\_MARKETING\_PLAYBOOK.md \# Commercial strategy & pricing tiers

│   └── PROGRESS\_REPORT.md           \# Cycle \#197 milestone report

├── screenshots/

│   └── fieldbus-studio-preview.svg  \# High-resolution SVG preview diagram

└── README.md                        \# Master product documentation

---

## 🚀 Quick Start

### 1\. Launch Interactive Web Studio

Open `product_197/source-code/index.html` in any web browser. Zero server, node packages, or build steps required.

### 2\. Standalone Python CLI Usage

\# Make CLI executable

chmod \+x product\_197/build/fieldbus-cli.py

\# Build an H1 Compelled Data (CD) Frame for Node 0x14 with PV \= 75.5

./product\_197/build/fieldbus-cli.py frame-build \--dst 0x14 \--src 0x01 \--type 1 \--pv 75.5

\# Dissect an H1 Hex Frame

./product\_197/build/fieldbus-cli.py frame-dissect "55 55 AC 01 14 01 42 97 00 00 80 69 DE AD"

\# Calculate an LAS Macrocycle Schedule

./product\_197/build/fieldbus-cli.py schedule \--loops '\[{"tag":"FIC-101","ai":25,"pid":35,"ao":25}\]' \--target 1000

\# Run 10-Point FF H1 Physical & LAS Safety Auditor

./product\_197/build/fieldbus-cli.py audit \--devices '\[{"addr":20,"spur":30,"ma":22,"lm":true}\]' \--trunk 600 \--psu 24.0

---

## 🧪 Verification & Automated Testing

The engine has been tested against 10 comprehensive unit tests:

python3 test\_foundationforge.py

\# Output: Ran 10 tests in 0.660s \- OK

---

## 💼 Commercial & Pricing Model

- **Community Edition**: Free / Open Source (Frame Builder, PV Quality Dissector, 2-Loop Scheduler, Web UI).  
- **Professional License**: \$299 one-time per engineer seat (Full Segment Voltage Sizer, 10-Point Safety Auditor, Python CLI, DeltaV / CENTUM Exporter).  
- **Plant Site License**: \$2,490 / facility / year (Site-wide multi-seat license, automated CI/CD segment validation hooks, FISCO barrier database, priority support).