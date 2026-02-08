# spec/plate30.md
# Plate30 Specification v1.0 (🦞30)

Status: LOCK INTENT  
Scope: Defines rules, validation modes, and reference panels for the `🦞30` travel format.  

---

## 1) Plate30 Definition

🦞30, or **Plate30**, is the default travel format for mobile and chat surfaces. It ensures:
- **Zero wrap** across constrained surfaces.
- Reliable **copy/screenshot survivability**.
- Predictable rendering behavior within 30-column boxes.

---

## 2) Width Law (🦞30)

### 2.1 Canonical Width Rule
- The total width of each panel line MUST be **≤30 columns**, including borders and padding.  

### 2.2 No Wrapping
- **Lines MUST NOT WRAP**, whether due to text overflow or rendering restrictions.
- If wrapping occurs or validation fails:
  - The panel becomes INVALID.
  - DO NOT PUBLISH or COPY invalid panels.
  - Revision or recompilation is REQUIRED.

### 2.3 Travel Format Standard
- Panels compiled to `🦞30` are safe to travel via chat clients, screenshots, or copy-paste.

---

## 3) Validation Canon

### 3.1 Validation Modes

#### **STRICT Mode (Travel or Compliance)**
- Content inside the box MUST BE ASCII-only (excluding borders).
- No emoji or jurisdiction opcodes (`📟`, `ℹ️`, etc.) are permitted inside the box.
- Validators must enforce width strictly using **codepoint counting**.

#### **RELAXED Mode (Controlled Surfaces Only)**
- Emoji MAY APPEAR inside the box, but validators must:
  1. Count emojis and variation selectors (e.g., VS16) explicitly as codepoints.
  2. WARN about potential rendering width drift.

### 3.2 Margin Law
- Each panel must include at least **one inner-space margin** between text and borders.
- Text MUST NOT touch the border.

---

## 4) Reference Panels

Below are **canonical 🦞30 examples** adhering to the specification.  

### Canonical width ruler (test)
0123456789012345678901234567|

### Canonical publish stamp (must travel with public copy payload)
📟 PUBLISHED · ærrivals / MCP64

### OPEN
┌────────────────────────────┐
│ ærrivals / MCP64           │
│                            │
│ OPEN                       │
│ READ ONLY                  │
│                            │
│ POWERED BY neuromitosis.com│
│ STEWARDED BY 🦞 NEURO       │
│ æææ IS ℹ️                   │
└────────────────────────────┘

### VERIFY
┌────────────────────────────┐
│ ærrivals / MCP64           │
│                            │
│ VERIFY                     │
│ SHA256: e3b0...b855        │
│                            │
│ POWERED BY neuromitosis.com│
│ STEWARDED BY 🦞 NEURO       │
│ æææ IS ℹ️                   │
└────────────────────────────┘

### ENTER
┌────────────────────────────┐
│ ærrivals / MCP64           │
│                            │
│ ENTER                      │
│ ▶️ MCP64 READY              │
│                            │
│ POWERED BY neuromitosis.com│
│ STEWARDED BY 🦞 NEURO       │
│ æææ IS ℹ️                   │
└────────────────────────────┘

### RUN
┌────────────────────────────┐
│ ærrivals / MCP64           │
│                            │
│ MCP64> RUN                 │
│ → SEALED                   │
│                            │
│ POWERED BY neuromitosis.com│
│ STEWARDED BY 🦞 NEURO       │
│ æææ IS ℹ️                   │
└────────────────────────────┘

### ERROR
┌────────────────────────────┐
│ ærrivals / MCP64           │
│                            │
│ ERROR                      │
│ PATH NOT VERIFIED          │
│                            │
│ POWERED BY neuromitosis.com│
│ STEWARDED BY 🦞 NEURO       │
│ æææ IS ℹ️                   │
└────────────────────────────┘

---

## 5) Jurisdiction Stamps (📟)

Every published panel MUST include its jurisdiction metadata:
- `📟` defines the **publisher** and **signature authority**.
- Example stamp:
  ```
  📟 PUBLISHED · ærrivals / MCP64
  ```

Rule: If it’s published, it MUST carry a stamp.

---

## 6) Ruler Check (Canonical Test)

Validate the editor/window width using this ruler:
```
0123456789012345678901234567|
```

---

## 7) Error Handling

When validation fails:
- Emit an **ERROR PANEL** and **REFUSE TO PUBLISH.**
- Panels MUST NOT travel if they fail validation.

---

## 8) Conclusion

Plate30 defines a portable, survivable format for conveying æ content under jurisdiction.