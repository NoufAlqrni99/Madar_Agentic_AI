# مَــدار | Madar
## Intelligent Multi-Agent Event Management System

> **Trainee:** Nouf Alqarni  
>
> **Training Programme:** Agentic AI Systems  
>
> **Delivered by:** SDAIA Academy  
>
> **Trainer:** Mohammed Albeladi  
>
> **Cohort Dates:** 23–27 August 2026  
>
> **Track:** Track A — Supervisor + Workers  
>
> **SDAIA Academy on GitHub:** https://github.com/SDAIAAcademy

---

## Project Description

Madar (مَدار) is an intelligent multi-agent system designed to support event operations and handle operational disruptions efficiently.

Event management involves multiple operational areas such as parking, schedules, and venue availability. Handling all of these tasks through a single agent can make decision-making less specialized and harder to manage.

Madar addresses this challenge through a Supervisor + Workers architecture. A central Supervisor Agent analyzes incoming requests and delegates them to specialized worker agents responsible for parking, scheduling, and venue operations.

The project demonstrates the main concepts covered in the Agentic AI Systems programme, including real tool calls, structured output, multi-agent orchestration, Agentic RAG, context and state management, human-in-the-loop workflows, reliability mechanisms, LangGraph Functional API, and LangSmith observability.

---

## Problem Statement

Event organizers may need to respond quickly to different operational issues during an event.

Examples include:

- Parking areas approaching full capacity.
- Speakers being delayed.
- Venue availability changing.
- Event policies needing to be retrieved quickly.
- Sensitive schedule changes requiring human approval.

A single general-purpose agent may not provide the specialization and control required for these different tasks.

Madar provides a coordinated multi-agent system where each operational request is delegated to the appropriate specialized agent while a Supervisor manages the overall workflow.

---

## System Objectives

Madar is designed to:

1. Route event-management requests to the appropriate specialized agent.
2. Perform real tool calls using operational event data.
3. Use structured output for predictable request classification.
4. Retrieve relevant operational policies through RAG.
5. Maintain short-term conversation state.
6. Store long-term facts across different conversation threads.
7. Require human approval before sensitive operational changes.
8. Handle transient failures using retry mechanisms.
9. Provide observable multi-agent execution through LangSmith.
10. Demonstrate a complete Supervisor + Workers agentic architecture.

---

## System Architecture

Madar follows **Track A — Supervisor + Workers**.

### Supervisor Agent

The Supervisor acts as the central orchestrator.

It analyzes incoming requests and delegates them to the appropriate specialized worker rather than using keyword-based routing.

### Worker Agents

- **Parking Agent** — handles parking status, capacity, and alternative parking recommendations.
- **Schedule Agent** — handles event schedules and speaker-delay situations.
- **Venue Agent** — handles hall availability, capacity, and venue-related information.

After completing a task, the worker returns control to the Supervisor.

---

## Workflow Pattern

The project implements the **Orchestrator–Worker** workflow pattern.

This pattern fits the problem because event operations contain several specialized domains while still requiring a single coordination point.

```text
                    User Request
                         |
                         v
                  Supervisor Agent
                         |
             +-----------+-----------+
             |           |           |
             v           v           v
         Parking      Schedule      Venue
          Agent        Agent        Agent
             |           |           |
             +-----------+-----------+
                         |
                         v
                  Supervisor Agent
                         |
                         v
                   Final Response
---

## Agent Fundamentals

Madar uses real tool calls to access and process operational event information. The agents select the appropriate tools based on the user's request rather than relying on hardcoded responses.

Structured output is implemented using Pydantic models and `with_structured_output` where routing or classification results need to be processed programmatically.

---

## Multi-Agent Architecture

The system follows **Track A — Supervisor + Workers**.

The Supervisor Agent coordinates the workflow and delegates requests to specialized Parking, Schedule, and Venue agents. Routing decisions are handled through the agentic workflow rather than keyword-based conditions.

---

## RAG Pipeline

Madar implements an **Agentic RAG** pipeline for retrieving event policies and operational knowledge.

Documents are:

1. Loaded into the system.
2. Split into manageable chunks.
3. Converted into embeddings using Hugging Face embeddings.
4. Stored in a FAISS vector store.
5. Retrieved according to the user's operational request.

Agentic RAG was selected because retrieval is performed when an agent determines that external operational knowledge is required.

---

## Context and State Management

Madar demonstrates both short-term and long-term memory.

- **Short-term memory:** maintains conversation state within the same thread using a checkpointer and `thread_id`.
- **Long-term memory:** stores persistent information separately so that relevant facts can be retrieved across different conversation threads.

A cross-thread test is included in the notebook to demonstrate persistence beyond a single conversation thread.

---

## Human-in-the-Loop

Sensitive operational actions, such as critical schedule changes, require explicit human approval before execution.

The workflow uses `interrupt()` to pause execution and `Command(resume=...)` to continue after an approval decision is provided.

This prevents irreversible or sensitive actions from being performed automatically.

---

## Reliability and Error Handling

Madar includes reliability mechanisms for handling failures during agent execution.

The project uses LangGraph Functional API concepts through `@task` and `@entrypoint`, together with error-handling strategies such as retry mechanisms for transient failures.

These mechanisms help make the multi-agent workflow more robust when tools or external operations fail temporarily.

---

## LangSmith Observability

LangSmith tracing is enabled to provide visibility into the execution of the multi-agent workflow.

Tracing makes it possible to inspect agent decisions, tool calls, routing behavior, and execution flow during development and debugging.

---

## How to Run

1. Open `Madar_Capstone_Final.ipynb` in Google Colab.
2. Run the installation and import cells.
3. Add the required API keys securely through **Google Colab Secrets**.
4. Do not place API keys directly in the notebook.
5. Run the notebook from top to bottom.
6. Execute the included demonstration cells to test the Supervisor, worker agents, RAG pipeline, memory, human approval workflow, reliability mechanisms, and tracing.

---

## Security

API keys and secrets are not stored in this repository.

Sensitive credentials should be configured through Google Colab Secrets or environment variables. The `.gitignore` file excludes common environment, secret, Python cache, and notebook-generated files.

---

## Technologies

- Python
- LangChain
- LangGraph
- LangSmith
- Hugging Face
- FAISS
- Pydantic
- Google Colab

---

## Training Programme

This capstone project was completed as part of the **SDAIA Academy — Agentic AI Systems** programme.

**Cohort:** 23–27 August 2026  
**Track:** Track A — Supervisor + Workers

SDAIA Academy on GitHub: https://github.com/SDAIAAcademy

---

## Author

**Nouf Alqarni**  
SDAIA Academy — Agentic AI Systems  
August 2026
