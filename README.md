## Nguyen Thanh Dat

I work on the plumbing under AI developer tooling — the API routers, session
stores, and configuration managers that sit between a coding agent and the
models it talks to. Mostly root-cause fixes in other people's codebases.

Every patch below ships with a regression test that I verify fails on `main`
before opening the pull request.

### Landed

| Project | | Work |
|---|---|---|
| [decolua/9router](https://github.com/decolua/9router) | ⭐25.7k | 6 commits in `main`. Hardened a client-IP trust path that accepted a spoofable header without proving it came from the socket ([`9225921`](https://github.com/decolua/9router/commit/9225921)). Fixed Gemini token accounting reading zero because usage sat inside the antigravity response envelope, and prompt-cache keys being dropped in Chat→Responses translation. |
| [lidge-jun/opencodex](https://github.com/lidge-jun/opencodex) | ⭐10.9k | 4 pull requests merged. Made the responses path [fail closed](https://github.com/lidge-jun/opencodex/pull/1788) when a routed provider invokes a tool that was never declared; normalized tool-call ids so cross-provider history replays. |
| [williamcachamwri/zalo-tg](https://github.com/williamcachamwri/zalo-tg) | ⭐276 | 5 pull requests merged. |

### In review

| Project | | Work |
|---|---|---|
| [farion1231/cc-switch](https://github.com/farion1231/cc-switch) | ⭐128k | [#6477](https://github.com/farion1231/cc-switch/pull/6477) — Codex Desktop's `[desktop]` config table was wiped on every provider switch. Also [#6474](https://github.com/farion1231/cc-switch/pull/6474), [#6476](https://github.com/farion1231/cc-switch/pull/6476), [#6479](https://github.com/farion1231/cc-switch/pull/6479). |
| [thedotmack/claude-mem](https://github.com/thedotmack/claude-mem) | ⭐91k | [#3619](https://github.com/thedotmack/claude-mem/pull/3619) — the OpenAI-compatible provider recorded every assistant reply into the conversation history twice, and nothing dedupes that history before it becomes the request's `messages` array, so the assistant half of every later request was double-billed. Also [#3620](https://github.com/thedotmack/claude-mem/pull/3620), [#3593](https://github.com/thedotmack/claude-mem/pull/3593). |
| [zenoamaro/react-quill](https://github.com/zenoamaro/react-quill) | ⭐7k | [#1050](https://github.com/zenoamaro/react-quill/pull/1050) — replace `findDOMNode` with a ref so the editor works on React 19. |
| [commandlineparser/commandline](https://github.com/commandlineparser/commandline) | ⭐4.8k | [#953](https://github.com/commandlineparser/commandline/pull/953) — retarget the test project to net8.0 so the suite runs on current SDKs. |
| [nestjsx/nestjs-typeorm-paginate](https://github.com/nestjsx/nestjs-typeorm-paginate) | ⭐875 | [#927](https://github.com/nestjsx/nestjs-typeorm-paginate/pull/927) — reject a limit of 0 instead of dividing `totalPages` by zero. |

### How I work

Most of these were found by reading code, not by reproducing a filed issue.
The expensive part is never the patch — it is reading enough of an unfamiliar
codebase to know which of five plausible causes is the real one. That is why
the diffs tend to be three lines rather than thirty.

I take review seriously in both directions. When a reviewer found two real
defects in my own diagnostic code on [claude-mem #3620](https://github.com/thedotmack/claude-mem/pull/3620),
I fixed both the same day and added tests for them rather than arguing.

### Day job

Fullstack — React/Next.js, NestJS, ASP.NET Core, MongoDB/Prisma/SQL. Based in
Thanh Hoa, Vietnam. Open-source work is evenings and weekends.

<sub>Contribution counts current as of August 2026.</sub>
