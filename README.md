<div align="center">

![Nguyen Thanh Dat — plumbing under AI developer tooling](./assets/header.svg)

[![Landed](https://img.shields.io/badge/landed-11_PRs_%2B_6_commits-d97757?style=flat-square&labelColor=161b22)](https://github.com/ntdatt812)
[![Open](https://img.shields.io/badge/open_for_review-28_PRs-8b949e?style=flat-square&labelColor=161b22)](https://github.com/ntdatt812)
[![Focus](https://img.shields.io/badge/focus-AI_developer_tooling-adbac7?style=flat-square&labelColor=161b22)](https://github.com/ntdatt812)
[![Location](https://img.shields.io/badge/Thanh_Hoa-Vietnam-adbac7?style=flat-square&labelColor=161b22)](https://github.com/ntdatt812)

</div>


I work on the plumbing under AI developer tooling — the API routers, session
stores, and configuration managers that sit between a coding agent and the
models it talks to. Almost all of it is root-cause work in codebases I did not
write.

Where the project has a test suite, every patch below ships with a regression
test that I verify fails on `main` before I open the pull request. Two of them —
the drawdb pull requests — do not, because that repository has no test runner at
all; those carry a written reproduction instead.

### Contribution record

Public data for [`ntdatt812`](https://github.com/ntdatt812), counted **2026-08-19**,
covering the preceding 12 months. "Landed" means the change is in the upstream
default branch of a repository I do not own — as a merged pull request, or as a
commit the maintainer cherry-picked from one.

| | Count | What it counts |
| --- | ---: | --- |
| Pull requests merged | **11** | Merged by maintainers of repos I don't own |
| Additional commits landed | **6** | In `decolua/9router` `main`; the PRs were closed and the work cherry-picked |
| Pull requests open | **28** | Awaiting maintainer review |
| Repositories | **11** | Third-party repos I've contributed to |

I am not a maintainer of any of these projects, and I don't claim to be.

### Landed

**[decolua/9router](https://github.com/decolua/9router)** — LLM API router, 25.7k★.
Six commits in `main`.

| Commit | What it does |
| --- | --- |
| [`9225921`](https://github.com/decolua/9router/commit/9225921) | Implements the hardening for [GHSA-5mj8-gf6m-fhw8](https://github.com/decolua/9router/security/advisories/GHSA-5mj8-gf6m-fhw8) (high): the router decided a request was local by trusting a client-supplied `X-9r-Real-Ip` header, so any remote caller could send `127.0.0.1` and reach the owner's LLM API with no key. Now the address must be proven to come from the socket. |
| [`70ba002`](https://github.com/decolua/9router/commit/70ba002) | Preserves `prompt_cache_key` when translating Chat into Responses — without it every routed request silently lost its cache hit. |
| [`59d858b`](https://github.com/decolua/9router/commit/59d858b) | Reads Gemini's `usageMetadata` out of the antigravity response envelope, so token accounting stopped reporting zero. |
| [`27f3710`](https://github.com/decolua/9router/commit/27f3710) | Ships `sql.js` in the Docker image so the pure-JS database fallback can actually start. |
| [`8af5e75`](https://github.com/decolua/9router/commit/8af5e75) | Adds Fish Audio as a text-to-speech provider. |
| [`b04c03c`](https://github.com/decolua/9router/commit/b04c03c) | Adds the Alibaba Token Plan provider (`token-plan.ap-southeast-1`). |

**[lidge-jun/opencodex](https://github.com/lidge-jun/opencodex)** — coding agent, 11k★.
Six pull requests merged.

| PR | What it does |
| --- | --- |
| [#1788](https://github.com/lidge-jun/opencodex/pull/1788) | Makes the responses path fail closed when a routed provider invokes a tool that was never declared, instead of passing it through. |
| [#1780](https://github.com/lidge-jun/opencodex/pull/1780) | Normalizes tool-call ids so conversation history replays across providers. |
| [#2042](https://github.com/lidge-jun/opencodex/pull/2042) | `noStructuredOutputModels` is documented, in seven locales, as an *exact* opt-out, and the Responses ingress enforces that. The native Chat passthrough matched the pre-colon prefix instead, so a `<listed>:<tag>` sibling the operator never opted out silently lost `response_format` and returned prose where JSON was expected. |
| [#2059](https://github.com/lidge-jun/opencodex/pull/2059) | Ten rows of the Lab behavior report tested list membership with a plain `includes`, while every runtime gate they describe matches through `modelInList`, which also accepts a bare entry for a tagged id. The report disagreed with production — and it is hashed into the behavior fingerprint that keys Lab evidence. |
| [#1806](https://github.com/lidge-jun/opencodex/pull/1806) | Keeps an absolute POSIX sqlite home literal in POSIX service files. |
| [#1805](https://github.com/lidge-jun/opencodex/pull/1805) | Gives the Windows test sandbox a real profile shape. |

**[williamcachamwri/zalo-tg](https://github.com/williamcachamwri/zalo-tg)** — Zalo↔Telegram bridge, 276★.
Five pull requests merged: [#42](https://github.com/williamcachamwri/zalo-tg/pull/42) group history backfill and offline auto-reply,
[#43](https://github.com/williamcachamwri/zalo-tg/pull/43) Zalo reactions as native Telegram reactions,
[#44](https://github.com/williamcachamwri/zalo-tg/pull/44) muted threads mirrored as silent,
[#45](https://github.com/williamcachamwri/zalo-tg/pull/45) typing and seen indicators,
[#46](https://github.com/williamcachamwri/zalo-tg/pull/46) message recall by reacting 🙈.

### Open for review

| Project | | Pull request |
| --- | --- | --- |
| [github/spec-kit](https://github.com/github/spec-kit) | 130k★ | [#4182](https://github.com/github/spec-kit/pull/4182) — a workflow `condition:` written without a `{{ }}` block is never evaluated: the string comes back untouched and any non-empty text is truthy, so `condition: inputs.count > 100` always takes the `then` branch and always loops to `max_iterations`. Rejects it at validation, and the suggested correction is checked to be loadable YAML. |
| [farion1231/cc-switch](https://github.com/farion1231/cc-switch) | 128k★ | [#6477](https://github.com/farion1231/cc-switch/pull/6477) — Codex Desktop's `[desktop]` config table was wiped on every provider switch. Also [#6474](https://github.com/farion1231/cc-switch/pull/6474), [#6476](https://github.com/farion1231/cc-switch/pull/6476), [#6479](https://github.com/farion1231/cc-switch/pull/6479). |
| [thedotmack/claude-mem](https://github.com/thedotmack/claude-mem) | 91k★ | [#3619](https://github.com/thedotmack/claude-mem/pull/3619) — the provider recorded every assistant reply into the conversation history twice, and nothing dedupes it before it becomes the request's `messages` array, so the assistant half of every later request was double-billed. Also [#3620](https://github.com/thedotmack/claude-mem/pull/3620), [#3593](https://github.com/thedotmack/claude-mem/pull/3593). |
| [drawdb-io/drawdb](https://github.com/drawdb-io/drawdb) | 39k★ | [#1115](https://github.com/drawdb-io/drawdb/pull/1115) — makes a real `pg_dump` file importable (closes [#852](https://github.com/drawdb-io/drawdb/issues/852)). Also [#1114](https://github.com/drawdb-io/drawdb/pull/1114), emitting the comma before inline foreign keys on SQLite export. |
| [tinyhumansai/openhuman](https://github.com/tinyhumansai/openhuman) | 36k★ | [#5583](https://github.com/tinyhumansai/openhuman/pull/5583) — the frontend documents one place to read config from, and nothing enforced it; adds the lint rule and fixes its one violation. |
| [decolua/9router](https://github.com/decolua/9router) | 25.7k★ | 13 open, including [#3369](https://github.com/decolua/9router/pull/3369) recovering a tool result that arrived without an id, and [#3368](https://github.com/decolua/9router/pull/3368) stopping a hard-coded heap cap from overriding the operator. |
| [lidge-jun/opencodex](https://github.com/lidge-jun/opencodex) | 11k★ | [#2077](https://github.com/lidge-jun/opencodex/pull/2077) — the same class of mismatch as [#2059](https://github.com/lidge-jun/opencodex/pull/2059), on the per-model override rows: the report read the map directly while the runtime reads it through a resolver that also falls back to the model family and folds case. |
| [zenoamaro/react-quill](https://github.com/zenoamaro/react-quill) | 7k★ | [#1050](https://github.com/zenoamaro/react-quill/pull/1050) — replace `findDOMNode` with a ref so the editor works on React 19. |
| [commandlineparser/commandline](https://github.com/commandlineparser/commandline) | 4.8k★ | [#953](https://github.com/commandlineparser/commandline/pull/953) — retarget the test project to net8.0 so the suite runs on current SDKs. |
| [nestjsx/nestjs-typeorm-paginate](https://github.com/nestjsx/nestjs-typeorm-paginate) | 875★ | [#927](https://github.com/nestjsx/nestjs-typeorm-paginate/pull/927) — reject a limit of 0 instead of dividing `totalPages` by zero. |

### How I work

Most of these were found by reading code, not by reproducing a filed issue. The
expensive part is never the patch — it's reading enough of an unfamiliar
codebase to know which of five plausible causes is the real one. That's why the
diffs tend to be three lines rather than thirty.

I apply the same standard to my own work, and reviewers do find things. On
[claude-mem #3620](https://github.com/thedotmack/claude-mem/pull/3620) a reviewer
found two real defects in my diagnostic code — a capped summary reply reported as
a truncated observation, and missing upstream usage rendered as zero output
tokens. On [openhuman #5583](https://github.com/tinyhumansai/openhuman/pull/5583)
a review caught that my lint selector was wrong in both directions: it missed
`import.meta['env']` entirely, because computed access stores the key somewhere
else on the node, and it flagged `new.target.env`, which is a different
meta-property. I reproduced each case before touching anything, then pinned the
boundary with a test that reads the selector out of the shipped config rather
than restating it. Fixes and tests the same day, in both cases.

I've also offered to take on verification work rather than only sending patches:
[claude-mem #3606](https://github.com/thedotmack/claude-mem/issues/3606#issuecomment-5325893081)
— checking each defect a tracker claims against current `HEAD` and reporting
which are already fixed and which are still live, for the maintainer to accept
or discard.

### Day job

Fullstack — React/Next.js, NestJS, ASP.NET Core, MongoDB/Prisma/SQL. Based in
Thanh Hoa, Vietnam. Open-source work is evenings and weekends.
