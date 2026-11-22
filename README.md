# ⚡ Stack Organization Simulator
### Computer Architecture — Stack-Based CPU Model

A fully interactive, browser-based simulator for learning **Stack Organization** as taught in Computer Architecture courses (based on Morris Mano / Hamacher / Tanenbaum syllabus).

---

## 📦 Project Files

```
StackOrganizationSimulator/
├── index.html       ← Main simulator (single self-contained file)
└── README.md        ← This file
```

## 🚀 How to Run

1. Open `index.html` in any modern browser (Chrome, Firefox, Edge)
2. No server, no install, no dependencies needed — it is fully self-contained!

---

## 🧠 Concepts Covered

| Concept | What it simulates |
|---|---|
| **Stack Pointer (SP)** | Points to top of stack, auto-increments/decrements |
| **Top of Stack (TOS)** | Always reflects the current top element |
| **LIFO Structure** | Last-In, First-Out memory access |
| **Accumulator** | Holds result after POP or arithmetic |
| **Status Flags (PSW)** | Z (Zero), N (Negative), C (Carry), V (Overflow) |
| **Stack Overflow** | Detected when pushing to a full stack |
| **Stack Underflow** | Detected when popping from an empty stack |
| **RPN Evaluation** | Reverse Polish Notation expression execution |

---

## 🔧 Features

### Stack Operations
| Button | ISA Opcode | Description |
|---|---|---|
| PUSH | 0x01 | Push immediate value onto stack |
| POP  | 0x02 | Pop TOS into accumulator |
| PEEK | 0x03 | Read TOS without changing SP |

### Arithmetic Operations (binary — pops 2, pushes 1)
| Button | Opcode | Effect |
|---|---|---|
| ADD | 0x10 | NOS + TOS |
| SUB | 0x11 | NOS − TOS |
| MUL | 0x12 | NOS × TOS |
| DIV | 0x13 | NOS ÷ TOS |
| AND | 0x14 | NOS & TOS |
| OR  | 0x15 | NOS \| TOS |
| XOR | 0x16 | NOS ^ TOS |
| NEG | 0x17 | −TOS (2's complement) |

### Stack Manipulation
| Button | Opcode | Description |
|---|---|---|
| SWAP | 0x20 | Swap TOS and NOS |
| DUP  | 0x21 | Duplicate TOS |
| ROT  | 0x22 | Rotate top 3 elements |
| OVER | 0x23 | Copy NOS to top |

### Views / Tabs
- **📊 Stack View** — Live LIFO cells with hex/decimal/binary display + CPU state canvas + statistics
- **💾 Memory Map** — 256-byte memory grid, stack region highlighted  
- **📖 ISA Reference** — Full instruction table with opcodes, stack effects, micro-operations, flag impacts
- **🔌 Circuit Diagram** — Hardware block diagram: PC, IR, MAR, MBR, ALU, Accumulator, SP, Flags, Stack Memory, Main Memory

---

## 🎓 How to Use for Learning

### Example 1: Basic PUSH/POP
```
PUSH 10   → SP = 0, TOS = 10
PUSH 20   → SP = 1, TOS = 20
PUSH 30   → SP = 2, TOS = 30
POP       → ACC = 30, SP = 1
POP       → ACC = 20, SP = 0
```

### Example 2: Arithmetic (stack-based)
```
PUSH 8     → [8]
PUSH 3     → [8, 3]
SUB        → [5]    (8 - 3 = 5)
PUSH 2     → [5, 2]
MUL        → [10]   (5 × 2 = 10)
```

### Example 3: RPN Expression
```
Expression: (3 + 4) * 2
RPN form:   3 4 + 2 *
→ Type "3 4 + 2 *" in the RPN Evaluator box
→ Click "RPN Eval" — watch it execute step by step
```

### Example 4: Infix Evaluation
```
Type "(5+3)*4" in Infix Eval
→ Converted automatically to RPN: [5, 3, +, 4, *]
→ Executed on the stack with animation
```

---

## 🏗️ Architecture Model

```
┌───────────────────────────────────────────────────┐
│                    CPU                             │
│  ┌──────────┐  ┌──────────┐  ┌──────────────────┐ │
│  │ PC       │  │ IR       │  │      ALU         │ │
│  │ (Prog Ctr│  │ (Instr   │  │  (Arithmetic     │ │
│  │  Register│  │  Reg)    │  │   Logic Unit)    │ │
│  └────┬─────┘  └────┬─────┘  └────────┬─────────┘ │
│       │              │                  │           │
│  ┌────┴─────┐  ┌────┴──────┐  ┌────────┴─────────┐ │
│  │ MAR      │  │Accumulator│  │  SP Register     │ │
│  │(Mem Addr │  │(ACC)      │  │  (Stack Pointer) │ │
│  │ Reg)     │  └───────────┘  └──────────────────┘ │
│  └────┬─────┘                                       │
└───────┼────────────────────────────────────────────┘
        │ Memory Bus
┌───────┴────────────────────────────────────────────┐
│                  STACK MEMORY                      │
│  Addr │ Value │  ← SP points here (TOS)           │
│  0x0F │  ---  │  15 (top address, empty)          │
│  0x0E │  ---  │  14                               │
│  ...  │  ...  │  ...                              │
│  0x01 │  ---  │  1                                │
│  0x00 │  ---  │  0 (bottom of stack)              │
└───────────────────────────────────────────────────┘
```

---

## 📋 Status Flags (Program Status Word — PSW)

| Flag | Bit | Set when |
|---|---|---|
| **Z** (Zero)     | PSW[0] | Result = 0 |
| **N** (Negative) | PSW[1] | Result < 0 (MSB = 1) |
| **C** (Carry)    | PSW[2] | Unsigned overflow (result > 255) |
| **V** (Overflow) | PSW[3] | Signed overflow (result > 127 or < −128) |

---

## 📝 Input Modes

The simulator supports three input formats for PUSH:
- **Decimal**: `-128` to `127` (signed 8-bit)
- **Hexadecimal**: `00` to `FF`
- **Binary**: `00000000` to `11111111`

---

## 🎨 Technology Stack

- **HTML5** — Structure
- **CSS3** — Animations, custom styling
- **Vanilla JavaScript** — All simulation logic
- **HTML5 Canvas** — CPU block diagram + Circuit diagram
- **Tailwind CSS** (CDN) — Utility classes

---

*Built for Computer Architecture studies — Stack Organization chapter*
