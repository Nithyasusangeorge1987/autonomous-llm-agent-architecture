# autonomous-llm-agent-architecture

# Multi-Layer Autonomous LLM Agent Architecture
### Simulating Layered Consciousness Through Specialized LLM Agents

> Master's Thesis — Paderborn Universität, 2026  
> Nithya Susan George | M.Sc. Computer Science Engineering  
> Research conducted at Fraunhofer IEM, Paderborn



## Overview

This thesis builds and evaluates a multi-layer AI architecture where 
each cognitive function — perception, emotion, reasoning, social 
awareness, ethics, self-reflection — is handled by a separate 
specialised LLM agent. The layers communicate through a shared 
Redis-backed blackboard and run continuously, not just when a user 
sends a message.

The core question:

> **Can AI systems reason, reflect, and adapt continuously across 
> multiple cognitive dimensions — rather than only responding 
> reactively to input?**



## Motivation

Current LLMs are powerful but fundamentally reactive. They respond 
to prompts. They do not think between messages, adapt over time, or 
reason across emotional, ethical, and cognitive dimensions 
simultaneously.

This project starts from a simple observation: human cognition is 
not a single process. It is layered — perception feeds emotion, 
emotion shapes reasoning, reasoning informs ethics and identity. 
Existing AI architectures collapse all of this into one model with 
one system prompt. The question this thesis asks is whether 
separating these layers into independent specialised agents produces 
something qualitatively different.

## Methodology

The work follows four main phases:

**Phase 1 — Literature and architecture review**  
Mapping existing multi-layer AI architectures and psychological 
models of cognition to identify design principles.

**Phase 2 — Layer design and implementation**  
Each layer is an independent LLM agent with its own system prompt, 
memory access, and output contract. The first 10 layers are 
prototypically implemented. Remaining layers are conceptually 
outlined.

**Phase 3 — Inter-layer communication**  
Layers communicate asynchronously via a Redis blackboard rather 
than direct calls. This decoupling is intentional — it allows 
parallel execution and prevents tight coupling between layers.

**Phase 4 — Evaluation**  
The system is tested in real scenarios to measure whether the 
layered architecture produces more robust, adaptive, and 
self-consistent behaviour than a single-model baseline.



## Architecture

### The Layer Stack

At least 10 layers are prototypically implemented. 
The remaining layers are conceptually outlined.
```
┌──────────────────────────────────────┐
│  Layer 10+   Self-Awareness          │  ← Metacognition, identity
├──────────────────────────────────────┤
│  Layer 6–9   Ethical / Social        │  ← Moral reasoning, social adaptation
├──────────────────────────────────────┤
│  Layer 3–5   Cognition               │  ← Reasoning, planning, self-reflection
├──────────────────────────────────────┤
│  Layer 2     Emotion / Affect        │  ← Affective state inference
├──────────────────────────────────────┤
│  Layer 1     Somatic / Perception    │  ← Surface-level input analysis
└──────────────────────────────────────┘
```

Each layer is an independent, specialised LLM-powered agent with 
its own system prompt, memory, and output contract. Layers 
communicate via a shared **Blackboard System** backed by Redis.



## Key Components

### Autonomous Cognition Loop

Agents do not wait for user input. Two mechanisms drive 
continuous internal activity:

- **Heartbeat System** — triggers reflection cycles every 30 
  seconds, generating context-aware internal thoughts based on 
  active goals, unresolved questions, emotional cues, and memory
- **Microloop System** — neuron-like firing patterns every 10 
  seconds where layers re-process their own or adjacent layer 
  outputs, simulating continuous low-level cognitive activity

### Agent State Machine

Each agent operates on a deterministic state machine to reduce 
LLM non-determinism:
```
IDLE → TASK_RECEIVED → PLANNING → EXECUTING → 
WAITING_TOOL → DONE / ERROR
```

Rule-based transitions enforce structured behaviour — for example, 
after reading an email, the agent is forced to check the calendar 
before scheduling, regardless of LLM output variability.

### Memory Architecture

| Store | Purpose |
|---|---|
| Redis Blackboard | Shared inter-layer memory |
| Agent Long-Term Memory | Past reflections tagged with emotion, cognition, perception metadata |
| Conversation History | Session-persistent dialogue context |
| Event Storage | Timestamped activity log |
| Virtual Environment | Task state and tool execution context |

### Tool Ecosystem

Agents autonomously interact with external systems:

- **Email** — read and manage emails
- **Calendar** — check availability, create and list events 
  (ISO-8601 and epoch timestamp parsing)
- **Filesystem** — file operations within virtual environment
- **Web Search** — real-time internet access
- **Tool Registry** — centralised registration and execution 
  with parameter validation and duplicate-execution guards



## Inter-Layer Communication

Layers do not call each other directly. They write outputs to the 
Redis-backed Blackboard and read from it asynchronously. This 
design enables:

- **Parallel processing** — multiple layers can run concurrently
- **Emergent behaviour** — higher layers build on lower layer 
  outputs without tight coupling
- **Fault isolation** — a failing layer does not block the system




## Tech Stack

| Component | Technology |
|---|---|
| Backend | FastAPI + Python |
| Frontend | React |
| State / Memory | Redis (blackboard, long-term memory, events) |
| LLM APIs | OpenAI GPT-4o, Anthropic Claude |
| Open Models | Llama, Mistral, Qwen (via LM Studio, self-hosted) |
| Containerisation | Docker Compose |
| Agent Framework | OpenClaw (self-hosted, planned Clawbot integration) |



## Research Context

This thesis is part of ongoing AI research at **Fraunhofer IEM, 
Paderborn**. It builds directly on production experience developing:

- LangGraph-based visual workflow engines
- Multi-agent orchestration frameworks with middleware stacks
- RAG pipelines with hybrid vector indexing (Qdrant)
- FastAPI backends for AI-driven enterprise automation
- Mobile AI applications with SSE streaming



## Status

🚧 **In Progress** — Target completion: 2026

> Implementation code is maintained in a private repository 
> due to research confidentiality at Fraunhofer IEM.  
> This repository documents the architecture, methodology, 
> and design decisions.



## Contact

**Nithya Susan George**  
M.Sc. Computer Science Engineering, Paderborn Universität  
[LinkedIn](https://www.linkedin.com/in/nithya-george-53b4a4257) | 
nithyageorge47542@gmail.com
