---
title: "Event 2: Capstone Solution Presentation"
date: 2026-07-25
weight: 1
chapter: false
pre: " <b> 4.2. </b> "
---

{{% notice warning %}}
**Note:** The information below is for reference purposes only. Please **do not copy it verbatim** into your report.
{{% /notice %}}

# Summary Report: Agentic AI Build Week and AWS Community Day Sharing Session

### Event Objectives

- Share the journey of building AI products on AWS from idea to demo-ready solution.
- Introduce practical problems that can be solved with Agentic AI, Computer Vision, and cloud-native architecture.
- Present how teams designed workflows, system architecture, cost models, and user experience.
- Share challenges in teamwork, MVP delivery under time pressure, and presenting a final product in front of an audience.
- Inspire participants who are new to hackathons, AWS experimentation, and AI product development.

### Teams and Presentation Topics

- **One Team**: A conversational ordering assistant for the KFC Bot Agent use case.
- **Plan V**: An AI-native app to support Solution Architects in requirement analysis, architecture proposal generation, diagram creation, and AWS cost estimation.
- **SignalScout**: A platform for detecting strategic business changes from data and evidence.
- **3KA**: A hackathon project called S.H.E.P.H.E.R.D. for crowd monitoring, congestion prediction, and operational response support.

## Key Highlights

### 1. From a chatbot to an AI agent that can take action

The One Team presentation focused on conversational commerce. The challenge was not only natural-language understanding, but also handling menu items, quantities, shopping-cart state, vouchers, promotions, order confirmation, and real operational risks caused by mistakes.

Their key distinction was:

```text
Chatbot
-> mainly answers questions

AI Agent
-> understands goals
-> plans
-> calls tools
-> updates real state
-> checks results
```

The KFC Bot Agent was positioned as a multi-channel ordering assistant that allows customers to place orders inside a messaging flow without switching applications or creating extra friction.

An important architectural lesson was to design once, but keep the system extensible enough to support more channels, more business contexts, and more capabilities later.

### 2. AI support for the work of a Solutions Architect

Plan V focused on a very realistic challenge: customers express requirements in natural language and expect an early architecture proposal, cost estimate, and technical recommendation quickly.

The traditional workflow often includes:

- Reading BRD or PRD documents
- Extracting requirements
- Identifying information gaps
- Drafting an architecture
- Revising the design
- Estimating costs
- Updating the solution based on feedback

Their proposed AI-native app supports:

- analyzing both natural-language and structured requirements
- generating a requirements catalog
- suggesting multiple high-level architecture options
- supporting hybrid-cloud architecture cases
- generating editable Draw.io diagrams
- using official AWS Architecture Icons
- estimating AWS cost by region
- listing assumptions, recommendations, and requirement gaps
- letting the user continue refinement through a chat interface

The most valuable point was that the solution was not trying to replace a Solutions Architect, but to create a faster and more reviewable first draft.

### 3. AI for detecting business strategy shifts

SignalScout addressed the problem of analyzing fragmented signals related to enterprise strategy and operations.

Its target users included:

- corporate strategy teams
- enterprise risk management teams
- competitive intelligence teams
- B2B enterprise account management teams

The platform focused on:

- detecting strategic changes
- identifying structured signals
- connecting isolated signals into a clear narrative
- analyzing financial and operational indicators
- building timelines, risk alerts, and future scenarios
- recommending whether to maintain, adapt, or accelerate strategic actions
- supporting conclusions with verifiable evidence

One especially strong point was the emphasis on **transparent and verifiable analysis**. AI was not expected to produce conclusions without evidence; instead, each conclusion needed to be linked back to data the user could inspect.

The team also compared multiple architecture and cost options, showing that AI system design must balance model choice with hosting cost, observability, security, and storage.

### 4. Hackathon experience through the S.H.E.P.H.E.R.D. project

The 3KA team presented their hackathon project:

> Smart Human-flow Evaluation, Prediction, Hazard Detection, Response, and Dispatch

The goal was to turn surveillance cameras into an operational intelligence source that can support decisions in real environments.

Main capabilities included:

- person detection and tracking
- crowd-density estimation
- congestion-status estimation
- bottleneck detection
- overload-risk prediction
- proactive alert generation
- support for workforce allocation decisions

The solution combined:

- YOLO and ByteTrack
- Amazon SageMaker
- Amazon Bedrock AgentCore
- Strands Agent
- a React monitoring dashboard

The agentic layer was divided into two roles:

#### Autonomous Monitor

- continuously observes crowd metrics
- detects congestion risks
- predicts overload pressure
- raises proactive alerts

#### Operator Copilot

- allows staff to ask questions in natural language
- answers using live metrics
- combines forecasting tools with operational recommendations

## What I learned

### Product-building mindset for AI systems

- A strong AI product starts from a real problem, not from the model or AWS service.
- AI only becomes valuable when it is connected to real data, business rules, and actual operational actions.
- A good demo needs to show a clear flow from input to output to user value.
- Agentic AI requires tools, guardrails, and verification rather than just fluent text generation.
- In enterprise use cases, AI conclusions should be backed by evidence whenever possible.

### Technical architecture lessons

- Splitting a system into independent modules makes it easier to scale, replace, and reuse components.
- Multi-channel architecture should rely on adapters instead of rewriting the entire business logic for each channel.
- AI workflows should separate understanding, planning, tool use, action, and verification.
- Observability is essential in distributed and AI-powered systems.
- Architecture choices must balance performance, scalability, security, and cost.

### MVP scope management

One lesson appeared clearly across the presentations:

> A smaller but complete MVP is more valuable than a bigger idea that does not actually run.

To deliver an MVP in a short time, teams need:

- a clear goal
- a concrete definition of done
- fewer features
- one strong end-to-end flow
- prepared accounts, templates, and tools
- clear ownership across coding, design, testing, and presenting
- demo preparation before the last minute

### Teamwork and delivery discipline

The teams also shared common challenges such as:

- members not knowing each other well at first
- unclear ownership
- forgotten commits
- code not working under time pressure
- limited AWS or AI experience
- late-night debugging
- accidentally exposing environment files in GitHub

These examples showed that DevOps and teamwork are not just about tools. Teams also need conventions for naming, branching, ownership, secret management, deployment checklists, rollback plans, and communication.

## Applying this to my own work

### For the DevOps role

- standardize repository, branch, and commit workflows
- separate environment configuration from source code
- never commit `.env`, credentials, or private keys
- set up CI checks before merge
- prepare infrastructure, accounts, and permissions early
- establish logging, metrics, and alerts from the beginning
- monitor cost for models, runtime, and infrastructure
- modularize the architecture so each member can work independently
- prepare both demo and cleanup checklists

### For current project work

- start from one small but complete end-to-end flow
- separate ingestion, processing, AI, and backend into clear modules
- define input, output, and contracts between groups
- always validate real results instead of trusting AI output by default
- design the system so data sources, models, or output channels can change without rewriting everything
- prepare dashboard or evidence artifacts that prove the system is actually working
- think about cost from the design stage, not only after implementation

## Event Experience

Participating in this event helped me better understand how an idea can be turned into an AI product that is actually demoable on AWS.

### Learning from multiple very different products

The four teams presented very different use cases:

- conversational commerce
- architecture automation
- strategic intelligence
- crowd monitoring

Even though the problems were different, they all shared the same deeper structure:

```text
Business problem
-> Data
-> AI reasoning
-> Tools or services
-> Verification
-> User value
```

This helped me realize that the value of AI is not only in the model itself, but in how the model is placed inside the larger system.

### Better understanding Agentic AI

From the presentations, I understood that Agentic AI is not simply a chatbot that responds fluently. A real agent needs:

- a goal
- context
- planning
- tools
- state
- action
- verification
- guardrails

Without these components, the system may generate impressive text but still fail to perform useful work reliably.

### Learning how to balance technical quality and demo-readiness

In a hackathon, teams do not have enough time to build full production systems. They need to choose the smallest core flow that proves:

- the problem is real
- the solution can run
- the architecture can extend
- the cost can be explained
- the demo clearly shows value

### Learning from small failures as well

Stories about broken code, forgotten commits, unclear ownership, and accidental secret exposure showed that operational mistakes can affect the final outcome just as much as technical design.

From a DevOps perspective, this reinforced the importance of:

- Git discipline
- secret management
- automation
- ownership
- observability
- preparation

## Final Takeaways

- It is not necessary to wait until everything feels perfect before joining a hackathon or building a solution.
- A team becomes stronger when members contribute complementary skills rather than identical strengths.
- Scope should stay narrow while the main flow becomes strong.
- Architecture must support change.
- AI should be connected to real data and real tools.
- AI output should be verified before it affects real systems.
- Cost and operations should be considered from the beginning.
- A clear demo is often more valuable than many unfinished features.

## Event Photos

I was very focused on following the presentations, listening to practical experience, and discussing ideas with teams and mentors, so I did not capture photos during the Capstone Presentation session.

Even without event photos, the technical insights, implementation stories, and product lessons were still the most valuable outcomes I gained. It also reminded me to prepare better for future events by recording both notes and key visual evidence.

> Overall, this event helped me see the full path from defining a problem to designing the architecture, building an MVP, controlling cost, preparing a demo, and working effectively as a team on AWS-based AI products.
