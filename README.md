## Nguyen Thanh Dat

I work on the plumbing under AI developer tooling — the API routers, session
stores, and configuration managers that sit between a coding agent and the
models it talks to. Almost all of it is root-cause work in codebases I did not
write.

Every patch below ships with a regression test that I verify fails on `main`
before I open the pull request.

### Contribution record

Public data for [`ntdatt812`](https://github.com/ntdatt812), counted **2026-08-18**,
covering the preceding 12 months. "Landed" means the change is in the upstream
default branch of a repository I do not own — as a merged pull request, or as a
commit the maintainer cherry-picked from one.

| | Count | What it counts |
| --- | ---: | --- |
| Pull requests merged | **9** | Merged by maintainers of repos I don't own |
| Additional commits landed | **6** | In `decolua/9router` `main`; the PRs were closed and the work cherry-picked |
| Pull requests open | **23** | Awaiting maintainer review |
| Repositories | **9** | Third-party repos I've contributed to |

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

**[lidge-jun/opencodex](https://github.com/lidge-jun/opencodex)** — coding agent, 10.9k★.
Four pull requests, all merged inside 24 hours.

| PR | What it does |
| --- | --- |
| [#1788](https://github.com/lidge-jun/opencodex/pull/1788) | Makes the responses path fail closed when a routed provider invokes a tool that was never declared, instead of passing it through. |
| [#1780](https://github.com/lidge-jun/opencodex/pull/1780) | Normalizes tool-call ids so conversation history replays across providers. |
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
| [farion1231/cc-switch](https://github.com/farion1231/cc-switch) | 128k★ | [#6477](https://github.com/farion1231/cc-switch/pull/6477) — Codex Desktop's `[desktop]` config table was wiped on every provider switch. Also [#6474](https://github.com/farion1231/cc-switch/pull/6474), [#6476](https://github.com/farion1231/cc-switch/pull/6476), [#6479](https://github.com/farion1231/cc-switch/pull/6479). |
| [thedotmack/claude-mem](https://github.com/thedotmack/claude-mem) | 91k★ | [#3619](https://github.com/thedotmack/claude-mem/pull/3619) — the provider recorded every assistant reply into the conversation history twice, and nothing dedupes it before it becomes the request's `messages` array, so the assistant half of every later request was double-billed. Also [#3620](https://github.com/thedotmack/claude-mem/pull/3620), [#3593](https://github.com/thedotmack/claude-mem/pull/3593). |
| [decolua/9router](https://github.com/decolua/9router) | 25.7k★ | 13 open, including [#3369](https://github.com/decolua/9router/pull/3369) recovering a tool result that arrived without an id, and [#3368](https://github.com/decolua/9router/pull/3368) stopping a hard-coded heap cap from overriding the operator. |
| [zenoamaro/react-quill](https://github.com/zenoamaro/react-quill) | 7k★ | [#1050](https://github.com/zenoamaro/react-quill/pull/1050) — replace `findDOMNode` with a ref so the editor works on React 19. |
| [commandlineparser/commandline](https://github.com/commandlineparser/commandline) | 4.8k★ | [#953](https://github.com/commandlineparser/commandline/pull/953) — retarget the test project to net8.0 so the suite runs on current SDKs. |
| [nestjsx/nestjs-typeorm-paginate](https://github.com/nestjsx/nestjs-typeorm-paginate) | 875★ | [#927](https://github.com/nestjsx/nestjs-typeorm-paginate/pull/927) — reject a limit of 0 instead of dividing `totalPages` by zero. |

### How I work

Most of these were found by reading code, not by reproducing a filed issue. The
expensive part is never the patch — it's reading enough of an unfamiliar
codebase to know which of five plausible causes is the real one. That's why the
diffs tend to be three lines rather than thirty.

I apply the same standard to my own work. On
[claude-mem #3620](https://github.com/thedotmack/claude-mem/pull/3620) a reviewer
found two real defects in my diagnostic code — a capped summary reply reported as
a truncated observation, and missing upstream usage rendered as zero output
tokens. I pushed fixes and tests for both the same day.

I've also offered to take on verification work rather than only sending patches:
[claude-mem #3606](https://github.com/thedotmack/claude-mem/issues/3606#issuecomment-5325893081)
— checking each defect a tracker claims against current `HEAD` and reporting
which are already fixed and which are still live, for the maintainer to accept
or discard.

### Day job

Fullstack — React/Next.js, NestJS, ASP.NET Core, MongoDB/Prisma/SQL. Based in
Thanh Hoa, Vietnam. Open-source work is evenings and weekends.
