# Module 00: DevOps Foundations & Mindset

## Why This Module

Diego has the technical depth — this module aligns that depth with DevOps philosophy so every subsequent tool is learned within the right mental model.

## Key Concepts

### DevOps is Not a Tool — It's a Practice

- Culture of shared responsibility between development and operations
- Breaking down silos (Diego has seen this from the ops/support side)
- Feedback loops: plan, code, build, test, release, deploy, operate, monitor

### The Three Ways

1. **Flow**: Optimize left-to-right delivery (dev to ops to customer)
2. **Feedback**: Amplify right-to-left feedback (monitoring, alerts, post-mortems)
3. **Continuous Learning**: Experimentation, risk-taking, repetition

### Infrastructure as Code Philosophy

- Declarative over imperative (describe the desired state, not the steps)
- Version everything — infrastructure changes go through the same review as code
- Immutable infrastructure: replace, don't patch (contrast with Diego's current patching work)

### GitOps

- Git as the single source of truth for infrastructure and application state
- Pull-based reconciliation vs push-based deployment
- Audit trail built into version control history

## Connection to Diego's Background

| Diego Already Knows | DevOps Extends This To |
|---|---|
| Manual server patching | Automated, immutable deployments |
| Incident bridge calls | Post-mortem culture, blameless reviews |
| Jira ticket workflows | Automated pipelines triggered by code changes |
| Log analysis (Splunk) | Observability platforms, SLOs, alerting |
| Hybrid cloud ops | Multi-cloud IaC, reproducible environments |

## Topics

0. **GitHub account setup and tooling** (see `github-setup.md`) — required before any other exercise
1. DevOps principles and cultural shifts
2. The DevOps toolchain overview
3. Development workflows (trunk-based vs GitFlow)
4. Environment strategy (dev, staging, production)
5. Documentation-as-code practices

## Module Deliverable

By the end of this module, the `devops-foundations` GitHub repository will exist with: skills matrix, environment setup docs, verification script, and a personal journey statement. This is the first piece of Diego's portfolio.
