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

Madar addresses this challenge through a **Supervisor + Workers** architecture. A central Supervisor Agent analyzes incoming requests and delegates them to specialized worker agents responsible for parking, scheduling, and venue operations.

The project demonstrates the main concepts covered in the Agentic AI Systems programme, including real tool calls, structured output, multi-agent orchestration, Agentic RAG, context and state management, human-in-the-loop workflows, reliability mechanisms, LangGraph Functional API, and LangSmith observability.

---

## Problem Statement

Event organizers may need to respond quickly to different operational issues during an event, such as:

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

The Supervisor acts as the central orchestrator. It analyzes incoming requests and delegates them to the appropriate specialized worker rather than using keyword-based routing.

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
```

---

## Agent Fundamentals

Madar uses real tool calls to access and process operational event information. The agents select the appropriate tools based on the user's request rather than relying on hardcoded responses.

Structured output is implemented using a **Pydantic model** with `with_structured_output` where routing information needs to be processed programmatically.

---

## Multi-Agent and Routing Architecture

The system follows **Track A — Supervisor + Workers**.

The Supervisor coordinates the workflow and delegates requests to the specialized Parking, Schedule, and Venue agents. Routing is performed through real agent handoffs rather than keyword-based `if` statements.

The executed workflow demonstrates both the handoff from the Supervisor to a worker and the return from the worker to the Supervisor.

---

## Agentic RAG Pipeline

Madar implements **Agentic Retrieval-Augmented Generation (RAG)** for event policies and operational knowledge.

The pipeline follows these stages:

1. Operational policy documents are loaded.
2. Documents are split into smaller chunks.
3. Embeddings are generated using Hugging Face Sentence Transformers.
4. The embeddings are stored in a FAISS vector store.
5. Relevant information is retrieved through semantic search.
6. Retrieval is exposed as a tool available to the agents.

**Agentic RAG** was selected because policy retrieval is required only for some operational questions. This allows an agent to retrieve additional knowledge when needed rather than forcing retrieval for every request.

---

## Context and State Management

Madar demonstrates both short-term state and long-term memory.

### Short-Term State

Short-term state is maintained using a LangGraph checkpointer with a `thread_id`. This allows information to persist across interactions within the same conversation thread.

### Long-Term Memory

Long-term facts are stored separately using a Store.

The notebook includes a cross-thread test demonstrating that a fact stored in one thread can still be retrieved from a different thread while short-term state remains thread-specific.

---

## Human-in-the-Loop

Madar includes human oversight for sensitive operational actions.

For a schedule change that should not be executed automatically, the workflow uses `interrupt()` to pause before applying the change.

After explicit approval is provided, `Command(resume="approve")` resumes the workflow and completes the action.

Both the interrupt and resume stages are demonstrated in the notebook.

---

## LangGraph Functional API and Error Handling

The project uses the **LangGraph Functional API** through:

- `@task`
- `@entrypoint`

Two reliability and error-handling strategies are demonstrated:

1. A real `RetryPolicy` handles a simulated transient connection failure and retries the operation.
2. Human interruption and approval are used for sensitive actions that should not be executed automatically.

This provides different handling strategies for different types of failures and operational risks.

---

## LangSmith Observability

LangSmith tracing is enabled for the multi-agent workflow.

Tracing provides visibility into:

- Supervisor execution.
- Worker-agent execution.
- Tool calls.
- Agent handoffs.
- Workflow execution.

The trace showed the Supervisor handoff and return path and demonstrated that multi-agent requests can involve several model interactions, making complex requests more token-intensive than focused requests.

---

## Technologies

- Python
- Google Colab
- LangChain
- LangGraph
- LangGraph Supervisor
- LangSmith
- Groq
- Pydantic
- Hugging Face Sentence Transformers
- FAISS

---

## Repository Structure

```text
Madar_Agentic_AI/
│
├── Madar_Capstone_Final.ipynb
├── README.md
└── .gitignore
```

- `Madar_Capstone_Final.ipynb` — main project notebook containing the implementation, demonstrations, captured outputs, evaluation, and rubric write-up.
- `README.md` — project description, technical documentation, and run instructions.
- `.gitignore` — excludes secrets and unnecessary generated files.

---

## How to Run

1. Open `Madar_Capstone_Final.ipynb` in Google Colab.
2. Add `GROQ_API_KEY` and `LANGSMITH_API_KEY` through **Google Colab Secrets**.
3. Grant the notebook access to both secrets.
4. Do not hard-code API keys inside the notebook.
5. Restart the runtime if necessary.
6. Run the notebook from top to bottom.
7. Review the captured outputs for each capstone demonstration.
8. Run the final evaluation section and verify that all checks pass.

---

## Capstone Requirements Demonstrated

### 1. Agent Fundamentals 
Real tool calls and Pydantic structured output using `with_structured_output` are demonstrated.

### 2. Multi-Agent / Routing Architecture 
**Track A — Supervisor + Workers** is implemented using LLM-driven agent handoffs rather than keyword matching.

### 3. RAG Pipeline 
Operational documents are loaded, split, embedded, stored in FAISS, and retrieved through Agentic RAG.

### 4. Context & State Management 
Short-term state uses a checkpointer and `thread_id`, while long-term facts are stored separately and verified through a cross-thread test.

### 5. Human-in-the-Loop 
Both `interrupt()` and `Command(resume=...)` are executed and demonstrated.

### 6. LangGraph Functional API & Error Handling 
The project uses `@task`, `@entrypoint`, a real `RetryPolicy`, and a separate human-approval strategy.

### 7. Workflow Pattern 
The project explicitly implements the **Orchestrator–Worker** pattern because event operations contain specialized domains coordinated by one Supervisor.

### 8. LangSmith Observability 
Tracing is enabled to inspect routing, tool calls, handoffs, and multi-agent execution.

---

## Security

API keys and credentials are not stored directly in this repository.

Sensitive credentials are configured through **Google Colab Secrets** and should never be hard-coded into the notebook, README, commits, or Git history.

The `.gitignore` file excludes common environment files, secrets, Python-generated files, and Jupyter notebook checkpoints.
