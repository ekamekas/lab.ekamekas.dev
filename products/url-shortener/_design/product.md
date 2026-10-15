# Product Brief: Self-Hosted URL Shortener

## Overview

Build an open-source, self-hosted URL shortener that aimed at developers and self-hosters

## Problem & Opportunity

Self-hosted shorteners today are either dated or heavy to run, which leaves room for a modern one with almost no setup. Shortening itself is a free commodity, so the value has to come from easy operation, analytics, and control over your own data.

- **Problem for self-hosters:** mature options (YOURLS, Shlink) feel dated or API-only; the modern open-source option (Dub) depends on several external services, so it is heavy to self-host
- **Problem for developers:** SaaS shorteners gate API volume, analytics and custom domains behind paid tiers, and the click data lives on someone else's servers.
- **Opportunity:** a single binary with minimal dependencies, fast startup and low memory, that runs on a small VPS or a Raspberry Pi and owns its click data.

## Target Users

The primary users are developers who run their own infrastructure and want short links under their own domain, controlled through an API.

| User | What they need | Priority |
| --- | --- | --- |
| Self-hosting developer / homelab user | One-command install, low resource use, safe upgrades, own domain | Primary |
| Developer integrating links into an app | REST API with keys, custom aliases, click data via API | Primary |
| Small team or company (internal links, branded links) | Multiple users, a simple web UI, link ownership | Later |
| Person clicking a link | Fast redirect, safe destination | Always (not a customer) |

Out of scope as target users: anonymous public users (abuse-heavy, no revenue), marketers needing campaign suites, and enterprises needing SSO and compliance at launch.

## Goals & Success Criteria

Success means a working public release by month 6 that teaches the stack, plus enough real usage to test a business model.

| Goal | Success criterion | Target |
| --- | --- | --- |
| Learn Tech Stack in depth | Core built  | Month 6 |
| Fast redirect | Cached redirect p95 under 10 ms on a small VPS | Month 6 |
| Easy self-hosting | Running from `docker compose up` in under 5 minutes | Month 6 |
| Small footprint | Native binary idle memory under 100 MB | Month 6 |
| Business research | One business model chosen and tested with real users or feedback | After month 6 |
| Adoption signal | First external users (GitHub stars, issues, installs) | After release |

## Similar Product Benchmark

The gap is a modern, lightweight self-hosted option; SaaS players compete on analytics, QR codes and branded domains.

| Product | Type | Positioning | Takeaway for this project |
| --- | --- | --- | --- |
| Dub | Open source + SaaS | Developer-first, modern analytics, affiliate tracking | Closest competitor; win on lighter self-hosting |
| Shlink | Self-hosted (PHP) | API-first, mature | Study its API and feature set |
| YOURLS | Self-hosted (PHP) | Long-running, plugin ecosystem | Shows demand; dated experience |
| Kutt | Self-hosted (Node) | Simple, clean | Simplicity is valued |
| Bitly | SaaS | Incumbent; links, QR, link-in-bio | Paid value = analytics, QR, domains |
| Short.io / Rebrandly | SaaS | Branded domains | Custom domains are a paid feature |

Standard expectations taken from this: custom aliases, click analytics, API access, QR codes, and custom domains.

## Functional Scope

The first release (Phases 1–3) is a single-admin, API-first shortener with click analytics and simple self-hosting; everything else comes after.

| Feature | Description | Phase |
| --- | --- | --- |
| Shorten URL | Create a short code for a long URL via API | 1 |
| Redirect | Resolve code and redirect; cached lookup | 1 |
| URL validation | Reject malformed URLs and loops to its own domain | 1 |
| Admin + API keys | One admin account; create and revoke API keys | 1 |
| Custom alias | User-chosen short code, with collision check | 2 |
| Expiring links | Optional expiry date or max clicks | 2 |
| Click tracking | Record timestamp, referrer, country, device without slowing the redirect | 2 |
| Analytics API | Clicks per link over time, top referrers, countries, devices | 2 |
| Link management | List, edit destination, disable, delete links | 2 |
| Packaging | Docker image, native binary, docker-compose, env-based config | 3 |
| Rate limiting | Per-API-key limits on link creation | 3 |
| Safety check | Optional Google Safe Browsing check on new links | 3 |
| Web UI | Minimal dashboard for links and stats | Later |
| QR codes | Generate QR for any short link | Later |
| Multi-user | Several users with their own links | Later |
| Custom domains | Multiple domains per instance | Later |

## Non-Goals

These are deliberately left out to fit 2 hours a week and keep the product light.

- **No hosted SaaS at launch:** no billing, plan tiers, or multi-tenant isolation. A hosted version is a later business experiment.
- **No public anonymous shortening:** each instance is run by its operator, who handles their own abuse.
- **No marketing suite:** no UTM builders, campaign management, or link-in-bio pages.
- **No mobile deep linking:** no iOS/Android SDKs or app-link verification.
- **No enterprise features at launch:** no SSO, audit logs, or role management.
- **No microservices:** one deployable, modular inside.

## Business Model Options

Start fully open source under AGPL, keep paid-feature boundaries clean in the code, and test a model only after the first release.

| Model | How it earns | Effort for you | Example |
| --- | --- | --- | --- |
| Pure open source | No revenue; portfolio and reputation | Lowest | YOURLS, Kutt |
| Open-core | Free AGPL core; paid license for team, SSO, audit, advanced analytics | Medium | Common in dev tools |
| Hosted version | Subscription for a managed instance of the same code | High (ops, billing) | Plausible, Dub |
| Source-available (BSL, fair source) | Commercial use requires a paid license | Medium; community pushback risk | Several dev tools since 2023 |
| Sponsorship / support | GitHub Sponsors, paid support contracts | Low, needs users first | Many OSS projects |

Hypotheses to test later:

1. Self-hosters will pay for team features (multi-user, SSO), not for core shortening.
2. Some users prefer a cheap hosted instance over running their own.
3. A light footprint is a strong enough reason to pick this over Dub or Shlink.
