<div align="center">

<img src="./assets/header.gif" width="100%" alt="Praveen Kumar — Full-Stack Engineer" />

<br/><br/>

[![Portfolio](https://img.shields.io/badge/praveenkumary.com-040806?style=for-the-badge&logoColor=00ff66&logo=globe)](https://praveenkumary.com)&nbsp;&nbsp;
[![GitHub](https://img.shields.io/badge/GitHub-040806?style=for-the-badge&logoColor=00ff66&logo=github)](https://github.com/praveen-kumary)&nbsp;&nbsp;
[![LinkedIn](https://img.shields.io/badge/LinkedIn-040806?style=for-the-badge&logoColor=00ff66&logo=linkedin)](https://linkedin.com/in/praveen-kumary)&nbsp;&nbsp;
[![Email](https://img.shields.io/badge/Contact-040806?style=for-the-badge&logoColor=00ff66&logo=gmail)](mailto:praveenkumar2000y@gmail.com)

</div>

<br/>

<div align="center">
<table>
<tr>
<td valign="top" width="58%">

### 🧑‍💻 &nbsp;About Me

I'm a software engineer who likes building clean, reliable web apps and contributing to the tools developers rely on every day.

- 🛠️ **Open Source**: Actively fixing bugs, improving edge-case handling, and shipping PRs to **Next.js**, **Cal.com**, **Astro**, **Prisma**, and **HMIS**.
- ⚡ **Daily Stack**: TypeScript, React, Next.js, TanStack, Node.js, Python, PostgreSQL, and Tailwind CSS.
- 🎯 **Engineering Focus**: Type safety, sub-millimeter UI alignment, sensible database schemas, and writing code that is straightforward to debug six months later.

</td>
<td valign="top" width="42%">

### ⚡ &nbsp;Core Tech Stack

<a href="https://skillicons.dev">
  <img src="https://skillicons.dev/icons?i=ts,nextjs,react,nodejs,tailwind,astro,python,fastapi,nestjs,java,postgres,redis,mongodb,mysql,prisma,graphql,docker,aws,linux,git,wordpress&perline=7&theme=dark" width="350" />
</a>

</td>
</tr>
</table>
</div>

<br/>

### 🌍 &nbsp;Open-Source Contributions & Fixes

```diff
+ sveltejs/kit              Reject binary remote form with empty file offsets (#17579) [MERGED]
+ calcom/cal.diy            Unused WhatsApp workflow strings (#30447) [MERGED]
+ hmislk/hmis               11 PRs merged: admissions, bills, reschedules, pharmacy, validation exceptions (#24898 - #24902, #24989 - #24994) [MERGED]
+ prisma/orm                Serialize queries in transactions (#30930), SQLite mutex leak (#30911), glob normalization (#30889)
+ TanStack/query            Skip redundant success dispatch on identical setQueryData (#12462)
+ withastro/flue            Transaction rollback guard (#893), message metadata (#894), image read tool (#895)
+ hmislk/hmis               Remove broken Antibiotics button (#24954), channel credit & reschedule bookings (#24955)
+ vercel/next.js            App directory path resolution in ESLint plugin (#100775), standalone server fixes (#100814)
+ withastro/astro           Component-rendered link tags in island output (#18535), route generator fallback (#18531)
+ calcom/cal.diy            Bookings overlay busy times & schedule accessibility (#30425, #30424)
```

<br/>

<details open>
<summary><b>🔬 &nbsp;Engineering Deep Dives & Systems Internals &nbsp;<i>(Click to expand / collapse)</i></b></summary>
<br/>

<table>
<tr>
<td>

#### 1. SvelteKit — Remote Form Binary Stream Boundary Validation ([#17579](https://github.com/sveltejs/kit/pull/17579)) · <kbd>MERGED</kbd>
- **The Challenge**: Malformed multipart form submissions containing non-printable character sequences and empty file slice byte offsets caused the SvelteKit Node adapter request parser to hang or produce unhandled stream rejections during server action dispatch.
- **Root Cause**: The stream decoder assumed boundary termination headers always contained contiguous CRLF delimiters without verifying against 0-byte sliced offsets on chunk boundaries.
- **Resolution**: Implemented early stream offset validation guarding against empty binary offsets prior to payload decoding, throwing a well-formed 400 Bad Request instead of choking the stream handler.

---

#### 2. Prisma ORM — Connection Socket Serialization in `@prisma/adapter-pg` ([#30930](https://github.com/prisma/orm/pull/30930))
- **The Challenge**: Under heavy concurrency during active database transactions, Node Postgres (`pg`) emitted deprecation warnings: *"Calling client.query() while another query is in progress is deprecated"*.
- **Root Cause**: `adapter-pg` passed incoming transaction queries directly to the underlying `pg.Client` without queue serialization, causing rapid async queries inside `$transaction` to overlap on the same raw TCP socket.
- **Resolution**: Engineered a promise-chained query queue directly inside the transaction driver wrapper, ensuring every query in the transaction resolves sequentially while maintaining non-blocking asynchronous pipeline flow. Verified across 56/56 Vitest integration test suites.

---

#### 3. Enterprise Java / HMIS — Transactional Rollback Semantics via `@ApplicationException` ([#24992](https://github.com/hmislk/hmis/pull/24992), [#24993](https://github.com/hmislk/hmis/pull/24993), [#24994](https://github.com/hmislk/hmis/pull/24994)) · <kbd>MERGED</kbd>
- **The Challenge**: In high-throughput hospital inventory and patient record services, invalid operational states (e.g. GRN approval with zero claimed items, patient record unmerges, cross-department requisition rejections) threw generic checked exceptions that failed to trigger container-managed EJB transaction rollbacks, leading to partial writes and database inconsistency.
- **Root Cause**: Standard Java exceptions caught inside JSF controllers bypassed container transaction demarcation unless explicitly annotated.
- **Resolution**: Created domain-specific business exceptions (`PatientMergeException`, `GrnApprovalException`, `ItemRequestException`) decorated with `@ApplicationException(rollback = true)`. This guarantees container-level rollback of all dirty JPA entity managers while surfacing clean, actionable localized UI error messages to hospital clinicians.

---

#### 4. TanStack Query — Redundant Dispatch Bypass on Deep-Equality Cache Update ([#12462](https://github.com/TanStack/query/pull/12462))
- **The Challenge**: Calling `queryClient.setQueryData` with an identical data structure repeatedly triggered observer re-renders and subscriber callback cascades across downstream React components.
- **Root Cause**: The query state transition machine emitted a `success` action regardless of whether the incoming state reference or deep structural clone had mutated.
- **Resolution**: Introduced a fast reference and shallow identity pre-check in `setQueryData` action dispatching to skip redundant notifications when cached data is functionally unchanged, cutting unnecessary DOM re-renders in heavy client dashboards.

</td>
</tr>
</table>

</details>

<br/>

### 🚀 &nbsp;Featured Projects &nbsp;·&nbsp; Engineering Portfolio

<div align="center">
<table>
<tr>
<td valign="top" width="50%">

### 💼 &nbsp;[Workforce OS](https://github.com/praveen-kumary/workforce-os)
**Unified Enterprise HR, Zero-Trust IT & Finance Platform**  
Modular enterprise operating system consolidating employee lifecycle management, Zero-Trust device fleet security, automated payroll runs, and BullMQ worker queues.

<br/>

<img src="https://img.shields.io/badge/TypeScript-3178C6?style=flat-square&logo=typescript&logoColor=white" />
<img src="https://img.shields.io/badge/React%2019-61DAFB?style=flat-square&logo=react&logoColor=black" />
<img src="https://img.shields.io/badge/Node.js%2020-339933?style=flat-square&logo=node.js&logoColor=white" />
<img src="https://img.shields.io/badge/Prisma-2D3748?style=flat-square&logo=prisma&logoColor=white" />
<img src="https://img.shields.io/badge/BullMQ-CC0000?style=flat-square&logo=redis&logoColor=white" />
<img src="https://img.shields.io/badge/Docker-2496ED?style=flat-square&logo=docker&logoColor=white" />

</td>
<td valign="top" width="50%">

### 🏍️ &nbsp;[MotoTribe](https://github.com/praveen-kumary/mototribe)
**India's Motorcycle Marketplace & Rider Community**  
Community-driven platform for motorcycle riders in India. Includes multi-seller gear & bike marketplace, community discussion boards, virtual garage tracker, and group ride event coordination.

<br/>

<img src="https://img.shields.io/badge/Next.js%2015-000?style=flat-square&logo=next.js&logoColor=white" />
<img src="https://img.shields.io/badge/NestJS-E0234E?style=flat-square&logo=nestjs&logoColor=white" />
<img src="https://img.shields.io/badge/PostgreSQL-4169E1?style=flat-square&logo=postgresql&logoColor=white" />
<img src="https://img.shields.io/badge/Redis-DC382D?style=flat-square&logo=redis&logoColor=white" />
<img src="https://img.shields.io/badge/Prisma-2D3748?style=flat-square&logo=prisma&logoColor=white" />

</td>
</tr>
<tr>
<td valign="top" width="50%">

### ⚡ &nbsp;[TradeFlow Platform](https://github.com/praveen-kumary/tradeflow-automation-platform)
**Event-Driven Automated Trading Engine**  
Algorithmic trading backend with worker execution queues, TimescaleDB for sub-second OHLCV time-series persistence, Redis pub/sub order streaming, and a live Next.js monitoring dashboard.

<br/>

<img src="https://img.shields.io/badge/Python-3776AB?style=flat-square&logo=python&logoColor=white" />
<img src="https://img.shields.io/badge/FastAPI-009688?style=flat-square&logo=fastapi&logoColor=white" />
<img src="https://img.shields.io/badge/TimescaleDB-FDB515?style=flat-square&logoColor=000" />
<img src="https://img.shields.io/badge/Redis-DC382D?style=flat-square&logo=redis&logoColor=white" />
<img src="https://img.shields.io/badge/Next.js-000?style=flat-square&logo=next.js&logoColor=white" />

</td>
<td valign="top" width="50%">

### 🤖 &nbsp;[JobsFlow AI](https://github.com/praveen-kumary/jobsflow-ai-aggregator)
**Job Aggregation & Extraction Pipeline**  
Multi-board job scraper with PostgreSQL `pg_trgm` fuzzy matching to eliminate duplicate postings, batch structured skill extraction, and a fast Turborepo search frontend.

<br/>

<img src="https://img.shields.io/badge/TypeScript-3178C6?style=flat-square&logo=typescript&logoColor=white" />
<img src="https://img.shields.io/badge/Next.js-000?style=flat-square&logo=next.js&logoColor=white" />
<img src="https://img.shields.io/badge/Turborepo-EF4444?style=flat-square&logo=turborepo&logoColor=white" />
<img src="https://img.shields.io/badge/PostgreSQL-4169E1?style=flat-square&logo=postgresql&logoColor=white" />

</td>
</tr>
<tr>
<td valign="top" width="50%">

### 📈 &nbsp;[ProfitMax Algo](https://github.com/praveen-kumary/profitmax-algo-trading)
**Quantitative Trading Engine for Indian Markets**  
Backtesting and execution system running automated rule-based and machine-learning strategies on NSE Nifty 50 symbols, featuring strict position sizing and drawdown stop rules.

<br/>

<img src="https://img.shields.io/badge/Python-3776AB?style=flat-square&logo=python&logoColor=white" />
<img src="https://img.shields.io/badge/FastAPI-009688?style=flat-square&logo=fastapi&logoColor=white" />
<img src="https://img.shields.io/badge/Pandas-150458?style=flat-square&logo=pandas&logoColor=white" />
<img src="https://img.shields.io/badge/NumPy-013243?style=flat-square&logo=numpy&logoColor=white" />

</td>
<td valign="top" width="50%">

### 🎬 &nbsp;[CineDhoom](https://github.com/praveen-kumary/cinedhoom)
**Pan-Indian Cinema Discovery Hub**  
Movie discovery platform tracking theatrical releases, streaming availability, and community ratings across Telugu, Tamil, Kannada, Malayalam, and Hindi cinema.

<br/>

<img src="https://img.shields.io/badge/Next.js-000?style=flat-square&logo=next.js&logoColor=white" />
<img src="https://img.shields.io/badge/TypeScript-3178C6?style=flat-square&logo=typescript&logoColor=white" />
<img src="https://img.shields.io/badge/Tailwind-06B6D4?style=flat-square&logo=tailwindcss&logoColor=white" />
<img src="https://img.shields.io/badge/TMDB%20API-01B4E4?style=flat-square&logo=themoviedatabase&logoColor=white" />

</td>
</tr>
</table>
</div>

<br/>

### 📊 &nbsp;GitHub Analytics &nbsp;&amp;&nbsp; Contribution Velocity

<div align="center">

<img width="48%" src="https://github-stats-extended.vercel.app/api?username=praveen-kumary&show_icons=true&theme=github_dark&hide_border=true&bg_color=040806&title_color=00ff66&icon_color=00ff66&text_color=c9d1d9&count_private=true&cache_seconds=1800" />
&nbsp;
<img width="48%" src="https://streak-stats.demolab.com?user=praveen-kumary&theme=dark&hide_border=true&background=040806&stroke=10b981&ring=00ff66&fire=00ff66&currStreakLabel=00ff66&cache_seconds=1800" />

<br/><br/>

<picture>
  <source media="(prefers-color-scheme: dark)" srcset="https://raw.githubusercontent.com/praveen-kumary/praveen-kumary/output/github-snake-dark.svg" />
  <source media="(prefers-color-scheme: light)" srcset="https://raw.githubusercontent.com/praveen-kumary/praveen-kumary/output/github-snake.svg" />
  <img alt="contribution snake" src="https://raw.githubusercontent.com/praveen-kumary/praveen-kumary/output/github-snake-dark.svg" />
</picture>

<br/><br/>

<sub>💡 Open for select consulting, high-impact engineering roles, and open-source collaborations · <b>Always Shipping</b></sub>

</div>
