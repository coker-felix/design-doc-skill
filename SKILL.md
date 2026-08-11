---
name: design-doc
description: Use when starting a complex, multi-person, or long-lived software project that needs a written design document before implementation. Use when asked to "write a design doc," "create a technical design," "draft an RFC," or when the project involves cross-team coordination, ambiguous requirements, or high-risk decisions where being wrong is expensive.
---

# Design Doc

## Overview

A design doc forces thinking through hard decisions before wasting time on the wrong implementation. It coordinates design choices among teammates and partner teams.

## When to Write One

Answer any of these "yes" → write a design doc. Two or more → definitely write one:

- Will multiple people coordinate to implement the design?
- Will the project take more than three months of full-time dev work?
- Will the implementation run in production for several years?
- Does the project involve cross-team collaboration?
- Are the goals and requirements of the project ambiguous?
- Are there catastrophic risks preventable at design time (security, legal)?

## What Belongs

**Rule of thumb:** What's the penalty for being wrong? If a decision is hard to reverse (language choice, data model, API contract), it belongs in the doc. If it's trivial to change later ("load more" vs infinite scroll), it doesn't.

## Components

Pick the subset relevant to your project.

### Objective
One sentence any stakeholder understands. Appears on page one.

> *Improve application performance by adding a caching layer between the web server and the database.*

### Background
Why this project? What problem does it solve? Previous attempts? Make the doc self-contained — readers may not hear your verbal explanation first.

### Goals / Non-goals
Goals define scope. Non-goals explicitly call out things readers might assume are in scope but aren't.

> **Non-goal:** Create a general-purpose reusable caching system. The cache makes app-specific optimizations.

### Scenarios
Paint a picture of the completed system in the real world. Walk through a user flow end-to-end.

> 1. Bob creates a custom report.
> 2. Bob clicks "Share > as URL."
> 3. Charlie clicks the link and sees Bob's report in read-only mode.

### Diagrams
Architecture diagrams, sequence diagrams, data flow. Visuals communicate structure faster than prose.

### Glossary
Define domain-specific terms so all readers share the same vocabulary.

### Constraints
Hard limits: technology choices, budget, timeline, regulatory requirements.

### SLOs / Monitoring / Alerting
What are the uptime, latency, throughput targets? How do you know the system is healthy? What triggers an alert?

### Interfaces
APIs, RPCs, data formats, CLI flags. Define the contract before implementation.

### Dependencies / Infrastructure
What does this depend on? Databases, queues, other services, third-party APIs.

### Security / Privacy / Legal
Auth model, data handling, compliance requirements. Catch catastrophic risks at design time.

### Logging
What critical events get logged? Log levels, retention, access control, PII exclusions.

### Alternatives Considered
Briefly list strong alternatives and why they were rejected. Preempt "why didn't you do X?" questions.

### Open Issues
Known unknowns. Decisions deferred. Gaps to resolve.

## Quick Reference: Sections by Priority

| Priority | Sections |
|----------|----------|
| Always | Objective, Background, Goals, Non-goals |
| Usually | Scenarios, Diagrams, Interfaces, Alternatives |
| High-risk projects | Security, Privacy, Legal, SLOs, Monitoring |
| Cross-team | Dependencies, Interfaces, Glossary, Timeline |

## Common Mistakes

| Mistake | Fix |
|---------|-----|
| Specifying every detail (writing the implementation) | Only include decisions where being wrong is expensive to fix |
| Skipping the Background because "everyone knows" | Write it anyway — new teammates and future you won't know |
| No Non-goals section | Explicitly call out things readers might assume are in scope |
| Arguing over trivial decisions in review | If it takes < a day to change, don't put it in the doc |
| No diagrams | Even a rough architecture sketch prevents misalignment |
