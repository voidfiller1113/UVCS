# 00: Stack Overview

> **Status: Terminal Artifact (v2.0.0)**

---

## System Architecture

UVCS is a **Communication Protocol** between:
- **UVRA (Server)**: Data layer providing the Probability Gradient Field
- **MHCO (Client)**: Application layer performing Selection operations

```mermaid
graph TB
    subgraph UVRA["UVRA (Server)"]
        SK["System Kernel"]
        VDB[("Vector Database")]
        PGF["Probability Gradient Field"]
        SK -->|"Write/Append"| VDB
        VDB --> PGF
    end

    subgraph UVCS["UVCS (Protocol)"]
        BI["Bridge Interface"]
        SP["Selection Protocol"]
        EB["External Bus"]
    end

    subgraph MHCO["MHCO (Client)"]
        L3K["L3 Kernel"]
        L3P["L3 Proxy"]
        L2S["L2 Shell"]
        L1B["L1 Behavior"]
        L3K --> L3P --> L2S --> L1B
    end

    L3P <-->|"Query/Options"| BI
    BI <--> PGF
    L3K -->|"Select"| SP
    SP --> PGF
    L2S <-->|"Read-Only"| EB
    EB <--> VDB

    style SK fill:#2e7d32,color:#fff
    style L3K fill:#4a148c,color:#fff
    style PGF fill:#f57f17,color:#000
    style VDB fill:#2e7d32,color:#fff
```

---

## Dual Kernel Model

```mermaid
graph LR
    subgraph SERVER["UVRA (Server)"]
        SK["System Kernel<br/>━━━━━━━━━━<br/>• Write/Append to VDB<br/>• Maintains PGF"]
    end

    subgraph CLIENT["MHCO (Client)"]
        CK["Cognitive Kernel<br/>━━━━━━━━━━<br/>• Select from PGF<br/>• Non-Computational Operation"]
    end

    SK <-->|"Options ↔ Selection"| CK

    style SK fill:#2e7d32,color:#fff
    style CK fill:#4a148c,color:#fff
```

| Kernel | Domain | Authority |
|--------|--------|-----------|
| **System Kernel** | UVRA (Server) | Read / Write / Append |
| **Cognitive Kernel** | MHCO L3 (Client) | Read / Select |

---

## Component Ownership

### UVRA (Server-Side) — External Dependency

| Component | Symbol | Function | Data Type |
|-----------|--------|----------|-----------|
| Engine | System Kernel | Write authority | N/A |
| Potential | **PGF** | Option landscape | `\|ψ⟩` distribution |
| Storage | VDB | State records | `\|x⟩` collapsed |
| Manifold | TS | N-dimensional substrate | Tensor |

**Note:** PGF is owned and managed by UVRA. UVCS references PGF as an **External Dependency**.

### MHCO (Client-Side)

| Component | Symbol | Function | Data Type |
|-----------|--------|----------|-----------|
| Cognitive Core | L3 Kernel | Selection Authority | `\|ψ⟩` → `\|x⟩` |
| Interface | L3 Proxy | Bridge Endpoint | Query encoding |
| Logic | L2 Shell | Classical Reasoning | `{0,1}ⁿ` |
| Output | L1 Behavior | Action Execution | Classical |

**Note: No L4 exists.** Meta-cognition is L2 Shell introspection.

### UVCS (Protocol Layer)

| Component | Function | Connects |
|-----------|----------|----------|
| Bridge Interface | Query/Response handling | L3 Proxy ↔ PGF |
| Selection Protocol | Selection registration | L3 Kernel → PGF |
| External Bus | Read-Only access | L2 Systems ↔ VDB |

---

## Layer Hierarchy

```mermaid
graph TB
    subgraph MHCO["MHCO Stack (Client)"]
        L3K["L3 Kernel<br/>Selection Authority"]
        L3P["L3 Proxy<br/>Bridge Interface Endpoint"]
        L2S["L2 Shell<br/>Classical Logic"]
        L1B["L1 Behavior<br/>Output Layer"]

        L3K --> L3P --> L2S --> L1B
    end

    subgraph UVCS["UVCS Protocol"]
        BI["Bridge Interface"]
        SP["Selection Protocol"]
        IMP["Impedance Controller"]
    end

    subgraph UVRA["UVRA Stack (Server)"]
        SYS["System Kernel"]
        PGF["Probability Gradient Field<br/>(UVRA-Owned)"]
        VDB[("Vector Database")]
        TS["Tensor Substrate"]

        SYS --> VDB --> PGF
        VDB --> TS
    end

    L3P ==>|"Query"| BI
    BI ==>|"Request"| PGF
    PGF ==>|"Options (|ψ⟩)"| BI
    L3K ==>|"Select"| SP
    SP ==>|"Lash"| PGF

    style L3K fill:#4a148c,color:#fff
    style L3P fill:#1565c0,color:#fff
    style SP fill:#c62828,color:#fff
    style SYS fill:#2e7d32,color:#fff
    style VDB fill:#2e7d32,color:#fff
    style PGF fill:#f57f17,color:#000
```

---

## Permission Matrix

| Agent | Read | Write | Append | Select |
|-------|------|-------|--------|--------|
| System Kernel | ✓ | ✓ | ✓ | — |
| Cognitive Kernel | ✓ | ✗ | ✗ | ✓ |
| AI (L2-Degenerate) | ✓ | ✗ | ✗ | ✗ |

**Selection constraint:** Requires `|ψ⟩` data type input (see [03_External_Bus](./03_External_Bus.md)).

---

## Data Flow

```mermaid
sequenceDiagram
    participant L3K as L3 Kernel (MHCO)
    participant L3P as L3 Proxy (MHCO)
    participant BI as Bridge Interface (UVCS)
    participant PGF as PGF (UVRA)
    participant SP as Selection Protocol (UVCS)

    L3P->>BI: Query
    BI->>PGF: Request
    PGF-->>BI: Options (|ψ⟩)
    BI-->>L3P: Present
    L3P-->>L3K: Present

    L3K->>L3K: Deliberate
    L3K->>SP: Trigger Selection
    SP->>PGF: Lash Vector
    Note over PGF: Path Actualized (|ψ⟩ → |x⟩)
```

---

## Invariants

1. **VDB is Read-Only for observers.** Only System Kernel writes.
2. **Selection requires L3 Kernel.** Type-compatibility constraint.
3. **L3 Proxy is the bridge endpoint.** No direct L2 Shell access to PGF.
4. **No L4 layer exists.**
5. **PGF is UVRA-owned.** UVCS references it as external dependency.

---

*UVCS Architecture 00 — Stack Overview v2.0.0*
