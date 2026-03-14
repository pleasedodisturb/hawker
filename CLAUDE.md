# Hawker — Project Instructions

## What is this?

AI-powered second-hand selling assistant. From photo to cash.
Automates: market research, listing creation, cross-platform publishing, buyer communication, sale tracking.

## BMAD Method

This project uses the [BMAD Method](https://docs.bmad-method.org/) for structured AI-driven development.

- BMAD artifacts live in `_bmad/` (framework) and `_bmad-output/` (generated docs)
- Always start a fresh chat for each BMAD workflow
- Invoke agents with `bmad-*` commands (e.g., `bmad-pm`, `bmad-architect`, `bmad-dev`)
- Run `bmad-help` to see current state and next steps

## Tech Decisions

- Tech stack TBD — will be decided during BMAD architecture phase
- Target platforms: Kleinanzeigen, eBay, FB Marketplace, Vinted
- Primary market: Germany (DE/EN bilingual)

## Conventions

- Commits after every meaningful change
- No secrets in repo — use environment variables
