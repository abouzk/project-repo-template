# -----------------PROJECT ARCHITECTURE.MD TEMPLATE-----------------------------

### Architecture.md Standard Structure
1. C4 Container Diagram
2. Concept of Operations (ConOps) [human-in-the-loop only]
3. Data Flow (detailed)
4. Sequence Diagram [complex interactions only]
5. State Machine [mode-based systems only]
6. Domain-Specific Diagram [rename per project]
7. Validation Pipeline [research/publication projects only]
8. Generalization Architecture [modular systems only]

---

### When to Use Each Diagram

| Diagram | Location | Use When | Skip When |
|---|---|---|---|
| C4 Context | README.md (always) | Every project | Never skip |
| Simplified Data Flow | README.md (optional) | Pipeline/simulation projects | Robot/hardware projects |
| C4 Container | architecture.md | Every project | Never skip |
| ConOps | architecture.md | Human-in-the-loop, medical robotics, safety-critical | Pure software pipelines, embedded firmware |
| Detailed Data Flow | architecture.md | Every project | Never skip |
| Sequence Diagram | architecture.md | Haptic loops, robot handoff sequences, ROS message chains, multi-component timed interactions | Simple pipelines, single-component systems |
| State Machine | architecture.md | Any system with distinct behavioral modes or states | Pure data pipelines with no mode switching |
| Validation Pipeline | architecture.md | Research projects targeting publication with quantitative results | Demos, tutorials, tooling |
| Generalization | architecture.md | Modularity is a core design claim | One-off projects, demos |

---

### Mermaid Templates

#### C4 Context (README.md)
```mermaid
graph TD
    subgraph External ["External Actors"]
        User((User /\nOperator))
        ExtData([External Data\nSource])
    end
    subgraph System ["System Name"]
        Core[Your System]
    end
    subgraph Output ["Outputs"]
        Out1([Output A])
        Out2([Output B])
    end
    User --> Core
    ExtData --> Core
    Core --> Out1
    Core --> Out2
```

#### Simplified Data Flow (README.md -- pipeline projects only)
```mermaid
flowchart LR
    A([Input]) --> B[Stage 1]
    B --> C[Stage 2]
    C --> D[Stage 3]
    D --> E([Output])
```

#### C4 Container (architecture.md)
```mermaid
graph LR
    subgraph LayerA ["Layer A"]
        A1[Component 1]
        A2[Component 2]
    end
    subgraph LayerB ["Layer B"]
        B1[Component 3]
        B2[Component 4]
    end
    A1 -->|data type| B1
    A2 -->|data type| B2
    B1 -->|feedback| A1
```

#### ConOps (architecture.md -- human-in-the-loop only)
```mermaid
flowchart LR
    subgraph Phase1 ["Phase 1: Setup"]
        A[Operator action] --> B[System response]
    end
    subgraph Phase2 ["Phase 2: Operation"]
        C[Trigger event] --> D[Autonomous action]
        D --> E[Human verification]
    end
    subgraph Phase3 ["Phase 3: Completion"]
        F[Handoff] --> G[Return to idle]
    end
    Phase1 --> Phase2
    Phase2 --> Phase3
```

#### Detailed Data Flow (architecture.md)
```mermaid
flowchart TD
    A([Input source]) --> B[Processing step]
    B --> C{Decision point}
    C -->|Path A| D[Process A]
    C -->|Path B| E[Process B]
    D --> F[Output stage]
    E --> F
    F --> G([Output])
    F -->|error| H[Error handling]
    H --> B
```

#### Sequence Diagram (architecture.md -- complex interactions only)
```mermaid
sequenceDiagram
    participant A as Component A
    participant B as Component B
    participant C as Component C
    A->>B: request(data)
    B->>C: forward(processed)
    C-->>B: response(result)
    B-->>A: return(output)
    Note over A,C: Repeat at N Hz
```

#### State Machine (architecture.md -- mode-based systems only)
```mermaid
stateDiagram-v2
    [*] --> Idle
    Idle --> Active : trigger condition
    Active --> Executing : confirmed
    Executing --> Idle : complete
    Executing --> Error : fault detected
    Error --> Idle : reset
    Active --> Idle : cancelled
```

#### Validation Pipeline (architecture.md -- research/publication only)
```mermaid
flowchart TD
    A[Run simulation] --> B[Extract results]
    B --> C[Compare to ground truth]
    C --> D{Within tolerance?}
    D -->|Yes| E[Validate parameters]
    D -->|No| F[Adjust parameters]
    F --> A
    E --> G[Publication results]
```

#### Generalization Architecture (architecture.md -- modular systems only)
```mermaid
flowchart TD
    Core[Core Pipeline\nunchanged across uses]
    Core --> UseCase1[Use Case A]
    Core --> UseCase2[Use Case B]
    Core --> UseCase3[Use Case C]
    subgraph Swappable ["Swappable Components"]
        S1[Component 1\nper use case]
        S2[Component 2\nper use case]
        S3[Component 3\nper use case]
    end
    Core --> Swappable
```

---
