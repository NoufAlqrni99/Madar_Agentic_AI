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
