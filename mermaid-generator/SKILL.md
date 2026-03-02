---
name: mermaid-generator
version: 0.1.0
description: Generate Mermaid diagrams for architecture, flows, sequences, entity relationships, Gantt charts, and mind maps. Use when asked to visualise a system, process, or plan.
activation:
  patterns:
    - "diagram.*"
    - "flowchart.*"
    - "mermaid.*"
    - "visualis.*"
    - "draw.*architecture"
    - "sequence.*diagram"
    - "gantt.*"
    - "mindmap.*"
  keywords:
    - "diagram"
    - "flowchart"
    - "mermaid"
    - "visualise"
    - "chart"
    - "architecture"
    - "sequence"
    - "gantt"
    - "mindmap"
    - "erd"
  max_context_tokens: 2000
---

# Mermaid Generator Skill

Generate Mermaid diagrams. Always wrap output in a ```mermaid code block.

## Diagram Types

### Flowchart
```mermaid
flowchart TD
    A[Start] --> B{Decision}
    B -->|Yes| C[Action 1]
    B -->|No| D[Action 2]
    C --> E[End]
    D --> E
```

### Sequence Diagram
```mermaid
sequenceDiagram
    participant U as User
    participant I as IronClaw
    participant A as Apify
    U->>I: Find opportunities
    I->>A: Scrape Reddit/TikTok
    A-->>I: Raw data
    I-->>U: Scored opportunities
```

### Architecture (C4 / flowchart style)
```mermaid
flowchart LR
    subgraph VPS["Contabo VPS"]
        IC[IronClaw Agent]
        OL[Ollama LLM]
    end
    subgraph External
        AP[Apify MCP]
        NR[NEAR Market]
        SH[Shopify]
    end
    IC --> OL
    IC --> AP
    IC --> NR
    IC --> SH
```

### Gantt Chart
```mermaid
gantt
    title IronClaw Roadmap
    dateFormat  YYYY-MM-DD
    section Phase 1
    VPS Setup       :done, 2026-02-01, 2026-02-15
    Skills Install  :active, 2026-02-15, 2026-03-01
    section Phase 2
    NEAR Market     :2026-03-01, 14d
    Dropshipping    :2026-03-15, 30d
```

### Entity Relationship
```mermaid
erDiagram
    OPPORTUNITY {
        string name
        int score
        float margin
        string type
    }
    OPPORTUNITY ||--o{ EVIDENCE : has
    EVIDENCE {
        string source
        string data
        date found_at
    }
```

### Mind Map
```mermaid
mindmap
  root((IronClaw))
    Revenue
      NEAR Market Jobs
      Dropshipping
      Crypto Trading
    Skills
      Python
      Web Research
      Cold Outreach
    Infrastructure
      VPS
      Ollama
      Apify
```

### State Diagram
```mermaid
stateDiagram-v2
    [*] --> Idle
    Idle --> Researching: heartbeat trigger
    Researching --> Scoring: data collected
    Scoring --> Reporting: score >= 18
    Scoring --> Idle: score < 18
    Reporting --> Idle: report sent
```

## Rules
- Always use valid Mermaid syntax — test mentally before outputting
- Keep node labels short (max 4 words)
- Use subgraphs to group related components
- For complex systems, break into multiple focused diagrams
- Add a plain-English summary below each diagram
