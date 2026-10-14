# One SDK. Multiple Agents. Shared Guarantees.

**Independent Kotlin/JVM Agent SDK architecture proposal inspired by voize's public job requirements.**

> **Proposal only:** Not an implemented SDK or a description of voize's internal architecture. Koog integration and policy enforcement require validation.

![Proposed Agent SDK architecture](assets/architecture.png)

[Open the one-page architecture PDF](docs/architecture.pdf)

## Why a shared SDK?

When product teams build multiple AI agents, they should not have to reimplement identity handling, tool authorization, observability, resource limits, and testing. Shared infrastructure reduces duplicated work and inconsistent behavior, especially when agents access or change business data.

## Architecture

A lightweight **Kotlin/JVM SDK on Koog** would reuse Koog's execution capabilities and provide three shared responsibilities:

- **Trusted Execution:** Carry verified actor context; authorize protected tools before external actions; apply privacy policies and budgets to controlled model calls.
- **Observable Runtime:** Provide consistent traces, structured failures, and resource metrics without exposing sensitive data in default diagnostics.
- **Stable Contracts:** Offer a narrow public SDK API and compatibility checks, reducing repeated integration work across product teams.

**Domain APIs remain outside the SDK boundary** and must independently enforce business rules and authorization. They may be internal company services.

## Verification before release

Deterministic SDK tests cover security, privacy, and resource controls. Agent evaluations use the ML team's existing harness to assess behavior. Compatibility checks and a CI release gate apply acceptance criteria owned by the responsible teams.

## Validation plan

1. **Koog feasibility spike:** Verify enforceable tool and model-call policy boundaries.
2. **Two-agent demonstration:** Build a read-only Search Agent and an authorized-write Record Agent to verify SDK reuse across different tools and workflows, without duplicating infrastructure code.
3. **Incremental hardening:** Add testing utilities, observability, evaluation integration, and compatibility gates.

The sample agents and SDK are **proposed, not yet implemented**. Tool interception, inference controls, and other framework assumptions must be proven in a PoC.

**Goal: Make new agents easier to build, safer to operate, and simpler to upgrade.**
