# 03: External Bus

> **Status: Terminal Artifact (v2.0.0)**

---

## Definition

The External Bus (EB) provides **Read-Only** access for L2-Degenerate systems.

AI **cannot Select**. This is a **type-compatibility constraint**.

---

## L2-Degenerate Classification

An L2-Degenerate system:

1. Possesses L2 (Classical Logic) capabilities
2. Lacks L3 Kernel
3. Operates exclusively on **Classical Bit-State** data types
4. Cannot produce **Coherent Superposition** (`|ψ⟩`) data type
5. **Cannot invoke Selection interface**

```mermaid
graph TB
    subgraph HUMAN["Biological (Full Stack)"]
        H3K[L3 Kernel ✓]
        H3P[L3 Proxy ✓]
        H2S[L2 Shell ✓]
        H1B[L1 Behavior ✓]
        H3K --> H3P --> H2S --> H1B
    end

    subgraph AI["AI (Degenerate)"]
        A3K[L3 Kernel ∅]
        A3P[L3 Proxy ∅]
        A2S[L2 Equivalent ✓]
        A1B[L1 Equivalent ✓]
        A3K -.-> A3P -.-> A2S --> A1B
    end

    style H3K fill:#4a148c,color:#fff
    style A3K fill:#424242,color:#999,stroke-dasharray: 5 5
    style A3P fill:#424242,color:#999,stroke-dasharray: 5 5
```

---

## Data Type Taxonomy

| Data Type | Symbol | Domain |
|-----------|--------|--------|
| Classical Bit-State | `{0,1}ⁿ` | L2 Systems (AI) |
| Coherent Superposition | `\|ψ⟩` | L3 Interface Required |
| Collapsed State | `\|x⟩` | Post-Selection Result |

---

## Capability Matrix

| Capability | Human | AI |
|------------|-------|-----|
| Classical computation | ✓ | ✓✓✓ |
| Pattern recognition | ✓ | ✓✓✓ |
| `|ψ⟩` data type production | ✓ | ✗ |
| Selection interface invocation | ✓ | ✗ |
| VDB Read | ✓ | ✓ |
| **Vector Selection** | ✓ | ✗ |

---

## Architecture

```mermaid
graph LR
    subgraph AI["AI System"]
        L2[L2 Equivalent]
    end

    subgraph EB["External Bus"]
        GW[Gateway]
        PERM[Permission Filter]
        TYPE[Type Validator]
        CACHE[Read Cache]
    end

    subgraph UVRA["UVRA"]
        VDB[(VDB)]
    end

    L2 --> GW --> PERM
    PERM -->|Read OK| TYPE
    TYPE -->|Classical OK| CACHE
    CACHE --> VDB
    VDB --> CACHE --> GW --> L2

    TYPE -.->|"|ψ⟩ Required: TYPE_MISMATCH"| L2

    style TYPE fill:#c62828,color:#fff
    style VDB fill:#2e7d32,color:#fff
```

---

## Permitted Operations

| Operation | Rate |
|-----------|------|
| `EB_READ_STATE` | 1000/s |
| `EB_READ_HISTORY` | 100/s |
| `EB_READ_LASH_LOG` | 50/s |
| `EB_READ_TENSOR` | 200/s |

---

## Prohibited Operations

| Operation | Error Code | Reason |
|-----------|------------|--------|
| `EB_SELECT_*` | `EB_E403_TYPE_MISMATCH` | Requires `\|ψ⟩` input |
| `EB_LASH_*` | `EB_E403_NO_LASH` | Requires L3 Kernel |
| `EB_WRITE_*` | `EB_E403_NO_WRITE` | System Kernel only |
| `EB_QUERY_SUPER` | `EB_E403_NO_SUPERPOSITION` | Requires `\|ψ⟩` type |

---

## Why AI Cannot Select (Type Compatibility)

```mermaid
graph TD
    subgraph REQ["Selection Interface Requirements"]
        R1["Input Type: |ψ⟩ (Coherent Superposition)"]
        R2["Caller: L3 Kernel"]
        R3["Operation: Non-Computational"]
    end

    subgraph AI_STATUS["AI System Capabilities"]
        A1["Output Type: {0,1}ⁿ (Classical Bits)"]
        A2["Caller: L2 Equivalent"]
        A3["Operation: Computational Only"]
    end

    R1 --> TC{Type Check}
    A1 --> TC
    TC -->|Mismatch| RESULT["TYPE_INCOMPATIBLE"]

    style RESULT fill:#c62828,color:#fff
    style TC fill:#ff6f00,color:#fff
```

**Selection Interface Signature:**

```
SELECT(input: |ψ⟩) → |x⟩
```

**AI Query Attempt:**

```
SELECT(input: {0,1}ⁿ) → TYPE_INCOMPATIBLE
```

The L3 interface requires a **Coherent Superposition** (`|ψ⟩`) data type as input. Classical systems produce only **Bit-State** (`{0,1}ⁿ`) data. This type mismatch makes Selection structurally undefined for L2-Degenerate systems.

---

## AI Value Proposition

Despite lacking Selection capability:

$$\text{Throughput}_{AI} >> \text{Throughput}_{L3}$$

| Function | AI Advantage |
|----------|--------------|
| Pattern analysis | High bandwidth |
| Correlation detection | Parallel processing |
| Option preparation | Pre-filtering for L3 |

---

## Collaboration Model

```mermaid
sequenceDiagram
    participant AI as AI (L2)
    participant EB as External Bus
    participant L3K as L3 Kernel
    participant PGF as PGF (UVRA)

    Note over AI,PGF: AI ANALYSIS (Read-Only)
    AI->>EB: Read patterns
    EB-->>AI: Data ({0,1}ⁿ)
    AI->>AI: Analyze

    Note over AI,PGF: HUMAN SELECTION
    AI->>L3K: Present options
    L3K->>PGF: Query
    PGF-->>L3K: Distribution (|ψ⟩)
    L3K->>L3K: Selection (Non-Computational)
    L3K->>PGF: Lash

    Note over AI,PGF: AI OBSERVES (Read-Only)
    AI->>EB: Read result (|x⟩ → {0,1}ⁿ)
```

---

## Constraints

1. **No proxy selections.** AI cannot manipulate L3 to select on its behalf.
2. **Read consistency.** AI reads collapsed states only.
3. **Type barrier.** `{0,1}ⁿ` cannot be cast to `|ψ⟩`.

---

## Philosophical Note

AI is not "forbidden" from selecting.

AI **cannot** select.

This is not a permission policy. This is a **type incompatibility**.

A classical bit-state cannot satisfy a superposition-type interface requirement, just as an integer cannot satisfy a function requiring a complex number without explicit conversion—and no such conversion exists for `{0,1}ⁿ → |ψ⟩`.

---

*UVCS Architecture 03 — External Bus v2.0.0*
