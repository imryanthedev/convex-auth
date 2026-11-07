# Convex Auth v2 — Open-source contribution opportunity report

**Repository:** [convex/convex-auth](https://github.com/convex/convex-auth)
**Branch analysed:** `reboot` at [`a7bdf81d`](https://github.com/convex/convex-auth/commit/a7bdf81d2eb8c63b9bf4d7a78e30b2402f07ea40) (2026-11-04)
**Research date:** 2026-11-05
**Data sources:** live GitHub API (`gh`), `git` history of `up/reboot` and all 100+ `up/*` remote branches, `KNOWN_ISSUES.md`, `AGENTS.md`, `CONTRIBUTING.md`, all 177 issues (open + closed), all 422 merged PRs, 519 closed-unmerged PRs, and 76 open PRs.

---

## 0. Executive summary (read this first)

**The brief's premise is only partly satisfiable.** Convex Auth does not run a v2 issue backlog:

- Zero open issues have **any assignee**. Labels exist but are sparse (23 of 98 open issues carry a label, 32 label applications in total; `enhancement` dominates). There are no issue templates.
- There are 25 open issues authored by Convex-affiliated accounts, but **none was opened in the v2 era** (v2 work began 2026-06-25). The newest is [#282](https://github.com/convex/convex-auth/issues/282) (Nicolapps, 2026-02-18, v1 docs site). The rest are 2024–2025 v1 backlog.
- Only **two open issues are aimed at the v2 line**: [#581](https://github.com/convex/convex-auth/issues/581) and [#796](https://github.com/convex/convex-auth/issues/796), both from external users.
- Maintainers work through PRs and the repo, not the tracker. Nicolapps has commented on **0** issues; dowski on 5 (v1-era); erquhart on 23 (mostly v1 support).

**However, one maintainer-authored issue is still exactly actionable:** [#30 "Add crons for cleaning up stale data"](https://github.com/convex/convex-auth/issues/30), opened by Convex co-founder **Michal Srb (`xixixao`)** on 2024-07-11, labelled `enhancement`, still open, unassigned, zero comments. erquhart explicitly closed the sibling issue [#17](https://github.com/convex/convex-auth/issues/17) saying *"Superseded by #30, which covers this along with other stale data cleanup."* v2 has since implemented parts of it (email challenges, passkey challenges) and is actively implementing another part (sessions), leaving a well-defined, unclaimed slice: **abandoned OAuth authorization requests and tickets**.

**Where the rest of the maintainer-authored backlog lives:** [`KNOWN_ISSUES.md`](https://github.com/convex/convex-auth/blob/reboot/KNOWN_ISSUES.md) (authored by Convex engineer **Shawn Erquhart / `erquhart`**) and explicit `TODO`/`FIXME` comments in `packages/core/src`. `KNOWN_ISSUES.md` opens with: *"Consciously deferred limitations, most should be addressed prior to v2 release."*

**Consequences for this report:**

1. Five of the ten "top verified opportunities" are anchored in numbered GitHub issues (#30, #581, #126/#350, #59/#755, #796); five are repo-documented gaps (four `KNOWN_ISSUES.md` entries and one code TODO). All are labelled by type. I have **not** invented issue numbers or statuses.
2. Many popular v1 issues (#619, #672, #674, #513, #457, #436, #355) are **already solved or structurally obsolete in v2** — verified against the source. They are listed in §3 so you do not waste time.
3. External PRs *have* been merged historically, but **only on `main`/v1**. As of 2026-11-05, **0 of the 292 PRs merged since v2 work began came from outside Convex** (§6). A short "is this wanted?" comment is therefore the rational first move — and this time there is a real issue to comment on.

**Single recommendation:** tackle [#30](https://github.com/convex/convex-auth/issues/30), scoped to the **OAuth authorization-request/ticket cleanup** that `KNOWN_ISSUES.md` §2 describes. It is the one combination of (maintainer-authored issue) + (explicit pre-GA known issue) + (zero PR/branch/assignee) + (real production impact) + (existing in-tree template).

---

## 1. Maintainers and core contributors

Counts are from the GitHub API on 2026-11-05. "v2 commits" = commits reachable from `reboot` but not `main` (288 total; author split below).

| GitHub | Name | Role / evidence | v2 commits | Merged PRs | Open PRs |
|---|---|---|---|---|---|
| [`Nicolapps`](https://github.com/Nicolapps) | Nicolas Ettlin | **Primary v2 maintainer.** GitHub company `@get-convex`; commits authored as `nicolas@convex.dev`; writes docs, password/email, passkey, OAuth client, CLI. | 202 | 219 | 42 |
| [`dowski`](https://github.com/dowski) | Christian Wyglendowski | **Core maintainer (sessions/auth core).** Commits authored as `christian@convex.dev`; owns session model, refresh, revocation, TOTP. | 69 | 80 | 18 |
| [`erquhart`](https://github.com/erquhart) | Shawn Erquhart | **Core maintainer (OAuth/SSR).** Bio: *"…Daylighting at The Final BaaS aka @get-convex"*; commits as `shawn@erquh.art` (not `@convex.dev`); authored `KNOWN_ISSUES.md` and most OAuth/SSR code. Employee status: strong evidence, **not** confirmed via org-membership API (`UNVERIFIED`). | 17 | 37 | 2 |
| [`ianmacartney`](https://github.com/ianmacartney) | Ian Macartney | Convex employee (profile company `Convex`); early core author and reviewer. | 0 | 3 | 2 |
| [`sethconvex`](https://github.com/sethconvex) | Seth Raphael | Convex employee; commits authored as `seth@convex.dev`; signing config, passkey hardening, session migration. | 1 (+ feature branches) | 1 | 2 |
| [`xixixao`](https://github.com/xixixao) | Michal Srb | **Convex co-founder** (`@get-convex`); original author; filed 35 issues, including [#30](https://github.com/convex/convex-auth/issues/30); now mostly historical. | 0 | 2 | 0 |
| [`thomasballinger`](https://github.com/thomasballinger) | Tom Ballinger | Convex employee (bio: *"…at Convex"*); historical v1 work; opened [#126](https://github.com/convex/convex-auth/issues/126). | 0 | 8 | 0 |
| [`sshader`](https://github.com/sshader) | Sarah Shader | Convex co-founder; 24 merged PRs, all v1-era; profile has no company field (`UNVERIFIED` via API, public knowledge). | 0 | 24 | 0 |
| [`reeceyang`](https://github.com/reeceyang) | Renee Yang | Convex employee (`@get-convex`); one open v2 refactor PR, no merges yet. | 0 | 0 | 1 |
| [`goffrie`](https://github.com/goffrie) | Geoffry Song | Convex employee (profile company `Convex`); one v1 PR merged. | 0 | 1 | 0 |

### Frequent external contributors (not maintainers)

| GitHub | Affiliation | Evidence |
|---|---|---|
| [`robelest`](https://github.com/robelest) | Trestle (external) | Draft PR [#797](https://github.com/convex/convex-auth/pull/797) adding WorkOS; 0 reviews, no maintainer comment. |
| [`saibotma`](https://github.com/saibotma) | Appella UG (external) | Filed [#755](https://github.com/convex/convex-auth/issues/755), [#756](https://github.com/convex/convex-auth/issues/756). |
| [`Hades32`](https://github.com/Hades32) | External | 2 merged v1 PRs ([#326](https://github.com/convex/convex-auth/pull/326), [#336](https://github.com/convex/convex-auth/pull/336)); two other proposals (#289, and the custom-claims change behind #298) were closed and later re-landed by a maintainer. |
| [`eden881`](https://github.com/eden881) | Lynx AI (external) | Merged v1 PR [#320](https://github.com/convex/convex-auth/pull/320) (2026-06-08 — the **last** non-Convex merge). |
| [`nyoung697`](https://github.com/nyoung697) | External | Merged v1 PR [#277](https://github.com/convex/convex-auth/pull/277). |
| [`focus-stefano`](https://github.com/focus-stefano) | External | PR [#280](https://github.com/convex/convex-auth/pull/280) closed unmerged; the feature (`beforeSessionCreation`) later landed as maintainer PR [#296](https://github.com/convex/convex-auth/pull/296). |

> ⚠️ Do not mistake `sethconvex`, `reeceyang` or `goffrie` for outsiders: their commit emails and/or profile companies are Convex.

---

## 2. Top 10 verified opportunities

Legend — **Type:** GH = GitHub issue, KI = `KNOWN_ISSUES.md` entry, TODO = code TODO.
**Status:** AVAILABLE = no open PR, no branch, no assignee, still reproducible; ASK FIRST = needs a maintainer decision before code; IN PROGRESS = an open PR/branch implements it.
**Priority:** P1 = maintainers say it should land before v2 GA / production correctness; P2 = meaningful; P3 = nice-to-have.
**Complexity:** S ≈ <½ day, M ≈ 1–2 days, L = design work / >2 days.

| # | Type | Ref | Title | Author | Date | Status | Priority | Complexity |
|---|---|---|---|---|---|---|---|---|
| 1 | GH | [#30](https://github.com/convex/convex-auth/issues/30) | Add crons for cleaning up stale data (v2 remainder: OAuth rows) | **xixixao (Convex co-founder)** | 2024-07-11 | **AVAILABLE** | P1 | M |
| 2 | TODO | [`email/validation.ts:27`](https://github.com/convex/convex-auth/blob/a7bdf81d2eb8c63b9bf4d7a78e30b2402f07ea40/packages/core/src/components/email/validation.ts#L27) | Accept internationalized email domains by encoding them to Punycode | **Nicolapps (Convex)**, via [#727](https://github.com/convex/convex-auth/pull/727) | 2026-10-15 | **AVAILABLE** | P2 | S/M |
| 3 | KI | [KNOWN_ISSUES §4](https://github.com/convex/convex-auth/blob/a7bdf81d2eb8c63b9bf4d7a78e30b2402f07ea40/KNOWN_ISSUES.md#L26-L35) | One pending OAuth flow per storage (concurrent tabs overwrite each other) | **erquhart (Convex)** | 2026-08-20 | **AVAILABLE** | P2 | L |
| 4 | GH | [#581](https://github.com/convex/convex-auth/issues/581) | Auth v2 password test helper fails to load Argon2 WASM in `convex-test` | nabilfatih | 2026-08-30 | **AVAILABLE** (docs/config, not a core bug — §3.4) | P3 | S |
| 5 | GH | [#126](https://github.com/convex/convex-auth/issues/126) + [#350](https://github.com/convex/convex-auth/issues/350) | TanStack Start / framework-agnostic SSR support | **thomasballinger (Convex)** / kevinkod | 2024-11-26 / 2026-06-08 | **ASK FIRST** (primitives landed; example+guide missing; [#350](https://github.com/convex/convex-auth/issues/350) has an unanswered claimant) | P2 | L |
| 6 | GH | [#59](https://github.com/convex/convex-auth/issues/59) + [#755](https://github.com/convex/convex-auth/issues/755) | Delete users / invalidate all sessions from outside the library | **xixixao (Convex)** / saibotma | 2024-08-21 / 2026-10-18 | **ASK FIRST** (v2 has partial equivalents, §3) | P3 | S/M |
| 7 | KI | [KNOWN_ISSUES §1](https://github.com/convex/convex-auth/blob/a7bdf81d2eb8c63b9bf4d7a78e30b2402f07ea40/KNOWN_ISSUES.md#L5-L7) | Rate limiting of all public routes | **erquhart (Convex)** | 2026-08-12 | **ASK FIRST** (partially done: password/email) | P1 | L |
| 8 | KI | [KNOWN_ISSUES §5](https://github.com/convex/convex-auth/blob/a7bdf81d2eb8c63b9bf4d7a78e30b2402f07ea40/KNOWN_ISSUES.md#L37-L49) | Support custom URL schemes (React Native `myapp://`, `exp://`) | **erquhart (Convex)** | 2026-08-12 | **ASK FIRST** (design decision) | P2 | L |
| 9 | GH | [#796](https://github.com/convex/convex-auth/issues/796) | v2 migration path from Better Auth (passwords, identity, TanStack, account switching) | primerch | 2026-10-29 | **IN PROGRESS** — scrypt migration is draft PR [#802](https://github.com/convex/convex-auth/pull/802); password length in [#803–#806](https://github.com/convex/convex-auth/pull/803) | P1 | L |
| 10 | KI | [KNOWN_ISSUES §6](https://github.com/convex/convex-auth/blob/a7bdf81d2eb8c63b9bf4d7a78e30b2402f07ea40/KNOWN_ISSUES.md#L51-L75) | Global sweep of retired refresh tokens | **erquhart (Convex)** | 2026-08-12 | **IN PROGRESS** — [#785](https://github.com/convex/convex-auth/pull/785), [#786](https://github.com/convex/convex-auth/pull/786), [#799](https://github.com/convex/convex-auth/pull/799) (dowski) | P1 | L |

### 2.1 Detail for the four genuinely available candidates

#### 1 — [#30](https://github.com/convex/convex-auth/issues/30): add crons for cleaning up stale data (AVAILABLE, best pick)

The issue body is only four lines:

> Crons are helpful for deleting:
> 1. expired verification codes (if user didn't authenticate)
> 2. expired sessions
> 3. _others? TODO_

Why it is still meaningful in v2:

- **`enhancement` label, zero comments, zero assignees.** No maintainer or external contributor has claimed it.
- **The sibling issue was explicitly folded into it.** erquhart closed [#17](https://github.com/convex/convex-auth/issues/17) on 2026-02-22 with *"Superseded by #30, which covers this along with other stale data cleanup."*
- **v2 has already delivered items 1 and 2**, which narrows the remaining scope:
  - email verification/challenge rows: [`components/email/cleanup.ts`](https://github.com/convex/convex-auth/blob/reboot/packages/core/src/components/email/cleanup.ts) (batch-worker loop, shipped in [#539](https://github.com/convex/convex-auth/pull/539));
  - passkey challenges: [`components/passkey/cleanup.ts`](https://github.com/convex/convex-auth/blob/reboot/packages/core/src/components/passkey/cleanup.ts);
  - sessions: [#785](https://github.com/convex/convex-auth/pull/785) / [#786](https://github.com/convex/convex-auth/pull/786) / [#799](https://github.com/convex/convex-auth/pull/799) (open, dowski).
- **The OAuth tables are the one stale-data class with no cleanup at all**, which `KNOWN_ISSUES.md` §2 spells out:

  > Expired authorization requests and tickets are only deleted when their secret is later presented (`packages/core/src/lib/oauth/dbHelpers.ts`), so abandoned flows accumulate forever.

Verified in current source:

- [`insertAuthorizationRequest`](https://github.com/convex/convex-auth/blob/a7bdf81d2eb8c63b9bf4d7a78e30b2402f07ea40/packages/core/src/lib/oauth/dbHelpers.ts#L57) writes a row with `expiresAt = now + 10 min` (`AUTHORIZATION_REQUEST_TTL_MS`, line 23).
- [`claimAuthorizationRequest`](https://github.com/convex/convex-auth/blob/a7bdf81d2eb8c63b9bf4d7a78e30b2402f07ea40/packages/core/src/lib/oauth/dbHelpers.ts#L97) deletes a row **only when the callback presents its `state`**.
- [`insertTicket` / `claimTicket`](https://github.com/convex/convex-auth/blob/a7bdf81d2eb8c63b9bf4d7a78e30b2402f07ea40/packages/core/src/lib/oauth/dbHelpers.ts#L132) do the same for tickets (2 min TTL).
- There is **no** `cleanup.ts` in `components/oauth`, `components/google`, `components/apple`, or `components/github`.
- Any anonymous caller can spam `startSignIn` (a public `mutationGeneric` with no identity check in [`lib/oauth/authorize.ts`](https://github.com/convex/convex-auth/blob/a7bdf81d2eb8c63b9bf4d7a78e30b2402f07ea40/packages/core/src/lib/oauth/authorize.ts#L82)), so growth is not merely organic.

Rating: **P1, M**. High production value, low ambiguity, but touches four components — post a scoping comment on #30 first (§7).

#### 2 — Punycode/IDN email domains (AVAILABLE, safest first PR)

[`email/validation.ts:27`](https://github.com/convex/convex-auth/blob/a7bdf81d2eb8c63b9bf4d7a78e30b2402f07ea40/packages/core/src/components/email/validation.ts#L27) says:

> `// TODO: accept internationalized domains by encoding them to Punycode.`

Introduced deliberately by Nicolapps in [#727](https://github.com/convex/convex-auth/pull/727) ("Reject email addresses that Resend cannot send to"), whose commit message ends: *"Internationalized domains could be supported later by Punycode-encoding them (left as a TODO)."* The test file currently asserts `a@exämple.com` is **rejected** ([`validation.test.ts:22`](https://github.com/convex/convex-auth/blob/a7bdf81d2eb8c63b9bf4d7a78e30b2402f07ea40/packages/core/src/components/email/validation.test.ts#L22)) — a PR flips that case and adds canonicalisation. Small, self-contained, maintainer-originated, directly unblocks international users.

Rating: **P2, S/M**.

#### 3 — Keyed pending OAuth flows (AVAILABLE, highest design risk)

[`methods/oauth/client.ts:168`](https://github.com/convex/convex-auth/blob/a7bdf81d2eb8c63b9bf4d7a78e30b2402f07ea40/packages/core/src/methods/oauth/client.ts#L168):

```ts
const OAUTH_FLOW_STORAGE_KEY = "flow";
```

One key per storage, so two tabs overwrite each other. `KNOWN_ISSUES.md` gives the fix direction (keyed flows selected by a **non-secret** flow id in the redirect URL; the `state` must still never be read from the URL). Server changes are needed too: `startSignIn` returns only `{ redirect, state }` today, and the callback builds its redirect in `redirectToApp`.

Rating: **P2, L**. Valuable, but it is login-CSRF-adjacent; get a design ack first.

#### 4 — [#581](https://github.com/convex/convex-auth/issues/581) password test helper WASM (AVAILABLE, but likely docs)

The repo's own [`vitest.config.ts`](https://github.com/convex/convex-auth/blob/a7bdf81d2eb8c63b9bf4d7a78e30b2402f07ea40/vitest.config.ts) already contains a `wasm-as-webassembly-module` plugin plus `server.deps.inline: ["convex-test", "argon2id-wasm"]`, added **2026-07-10** ([#390](https://github.com/convex/convex-auth/pull/390)) — seven weeks *before* the issue. CI runs the very same helper in [`examples/react-password/convex/password.test.ts`](https://github.com/convex/convex-auth/blob/reboot/examples/react-password/convex/password.test.ts) and [`examples/react-email-password/convex/emailPassword.test.ts`](https://github.com/convex/convex-auth/blob/reboot/examples/react-email-password/convex/emailPassword.test.ts). The report's `Cannot find package 'wbg'` error is exactly what the plugin's comment says it prevents.

Conclusion: **the library helper is not broken in the repo's supported setup**; the issue is a consumer Vitest configuration gap. A contribution here is a documentation/troubleshooting page ("Testing the password component with Vitest + convex-test") rather than a code fix. Still open, unassigned, no PR, no cross-reference — **AVAILABLE, P3, S**.

---

## 3. Issues that look relevant but are not (verified against `reboot`)

This is the part that saves you from duplicated or pointless work. Each row was checked in source at `a7bdf81d`.

| Issue | Why it is not a v2 task |
|---|---|
| [#674](https://github.com/convex/convex-auth/issues/674) JWKS `max-age=15` | **NOT RELEVANT TO V2.** v2 mints **deployment-issued** JWTs (`ctx.auth.signJwt`, [#787](https://github.com/convex/convex-auth/pull/787)). `convexAuthProvider` points at `${CONVEX_CLOUD_URL}/.well-known/jwks.json` ([`server/authProvider.ts:40`](https://github.com/convex/convex-auth/blob/a7bdf81d2eb8c63b9bf4d7a78e30b2402f07ea40/packages/core/src/server/authProvider.ts#L40)); the library serves no JWKS route and sets no cache header. The TTL is Convex-platform behaviour, not this repo's. |
| [#672](https://github.com/convex/convex-auth/issues/672), [#619](https://github.com/convex/convex-auth/issues/619) Apple/iPad cookie failures | **NOT RELEVANT TO V2.** The v2 OAuth flow uses **no cookies**. `state`, `codeVerifier`, `redirectTo`, and the provider config are stored server-side in the component's `authorizationRequests` table and claimed by state hash ([`lib/oauth/authorize.ts`](https://github.com/convex/convex-auth/blob/a7bdf81d2eb8c63b9bf4d7a78e30b2402f07ea40/packages/core/src/lib/oauth/authorize.ts), [`callback.ts`](https://github.com/convex/convex-auth/blob/a7bdf81d2eb8c63b9bf4d7a78e30b2402f07ea40/packages/core/src/lib/oauth/callback.ts)). `grep -i cookie` over the whole OAuth layer returns **zero** hits. Apple's `form_post` is handled explicitly via `callbackMethod: "POST"` → `response_mode=form_post`. |
| [#513](https://github.com/convex/convex-auth/issues/513) silent callback failure | **NOT RELEVANT TO V2.** v2 redirects back with a normalized `oauth_error` param (`expired`, `oauth_error`, `access_denied`, provider error codes) — see `redirectToApp` and the `catch` at the end of `handleOAuth` in [`lib/oauth/callback.ts`](https://github.com/convex/convex-auth/blob/a7bdf81d2eb8c63b9bf4d7a78e30b2402f07ea40/packages/core/src/lib/oauth/callback.ts#L449-L458). Finding 1 is fixed by design; finding 2 (cookie withholding) cannot occur because there is no cookie. |
| [#457](https://github.com/convex/convex-auth/issues/457) literal `code_verifier=decoy` | **NOT RELEVANT TO V2.** The verifier is persisted with the authorization request and passed back to the exchange (`authRequest.codeVerifier`); v2 sends no sentinel because every flow gets PKCE and a stored verifier. |
| [#304](https://github.com/convex/convex-auth/issues/304) Entra multi-tenant issuer | **NOT RELEVANT TO V2 (as filed).** v2 has no built-in Microsoft component; the generic `oauth` component accepts an explicit `issuers` array on the authorization request ([`components/oauth/schema.ts`](https://github.com/convex/convex-auth/blob/reboot/packages/core/src/components/oauth/schema.ts)) and validates against it. |
| [#436](https://github.com/convex/convex-auth/issues/436) `useInMemoryStorage` write-only | **NOT RELEVANT TO V2.** Replaced by a class-based [`InMemoryStorage`](https://github.com/convex/convex-auth/blob/a7bdf81d2eb8c63b9bf4d7a78e30b2402f07ea40/packages/core/src/browser/storage.ts#L58) with a real backing object; `storage="inMemory"` is gone. |
| [#355](https://github.com/convex/convex-auth/issues/355) prototype pollution in provider merge | **NOT RELEVANT TO V2.** v2 removed `@auth/core` provider option merging and the `src/server/provider_utils.ts` code path entirely; providers are typed component catalogs. |
| [#363](https://github.com/convex/convex-auth/issues/363) refresh throws → stopped socket | **NOT RELEVANT / UNVERIFIED.** v2 replaced the client with `browser/sessionManager.ts`, which wraps refresh in `retryOnNetworkError` and never leaves an unhandled rejection by design. No v2 reproduction was attempted; label `UNVERIFIED` if you rely on it. |
| [#756](https://github.com/convex/convex-auth/issues/756) / [#176](https://github.com/convex/convex-auth/issues/176) Email provider ctx/metadata | **NOT RELEVANT TO V2.** v2's email path is not Auth.js `EmailConfig`; it takes a Resend `sendEmail` function reference and runs it through the component ([`methods/email-password/server.ts`](https://github.com/convex/convex-auth/blob/reboot/packages/core/src/methods/email-password/server.ts)). There is no `sendVerificationRequest`. |
| [#282](https://github.com/convex/convex-auth/issues/282) docs tabs auto-switch | **NOT RELEVANT TO V2** (and not a code task). It targets the v1 docs at `labs.convex.dev/auth`. The v2 docs have moved to a Docusaurus site under `packages/docs/`. |
| [#334](https://github.com/convex/convex-auth/issues/334) too many reads | **PARTIALLY ADDRESSED / IN PROGRESS.** v2 caps sessions per user at 100 ([#783](https://github.com/convex/convex-auth/pull/783)) and is actively rewriting refresh-token lifetime/cleanup ([#798](https://github.com/convex/convex-auth/pull/798), [#799](https://github.com/convex/convex-auth/pull/799)). Not a good external task now. |
| [#323](https://github.com/convex/convex-auth/issues/323) `maxFailedAttempsPerHour` typo | **NOT RELEVANT TO V2.** The key does not exist anywhere in v2 (`grep` over `packages/core/src` returns nothing). |
| [#755](https://github.com/convex/convex-auth/issues/755) `invalidateSessions` from a mutation | **PARTIALLY ADDRESSED.** v1's function does not exist in v2. v2 has `components.auth.public.revokeSessions({ sessionIds })` ([`component/public.ts:636`](https://github.com/convex/convex-auth/blob/a7bdf81d2eb8c63b9bf4d7a78e30b2402f07ea40/packages/core/src/component/public.ts#L636)), callable from an app mutation, and `ctx.convexAuth.revokeAllSessions(userId)` inside method handlers. What is missing is a *public app-level* helper; that is an API-design decision. Note [#59](https://github.com/convex/convex-auth/issues/59) cross-references it. |
| [#179](https://github.com/convex/convex-auth/issues/179), [#180](https://github.com/convex/convex-auth/issues/180), [#58](https://github.com/convex/convex-auth/issues/58) Next.js v1 issues | **NOT RELEVANT TO V2** as filed. v2 replaced the Next.js integration (`ssr/nextjs/`) and no longer depends on `@auth/core`; the specific v1 mechanisms in these reports no longer exist. |

---

## 4. PR / branch overlap audit

### 4.1 Global checks performed

- `gh pr list --state all` → **422 merged**, **519 closed-unmerged**, **76 open**.
- Full-text PR search for: `cleanup`, `authorizationRequests`, `oauth cleanup`, `pending flow`, `flow id`, `keyed flow`, `rate limit`, `punycode`, `custom scheme`, `React Native`, `startSignIn`, `invalidateSessions`, `sendVerificationRequest`, `wasm`, `argon2`, `convex-test`, `test helper`, `crons`.
- `git log --grep` on `reboot` for: `punycode`, `internationalized`, `cleanup`, `pending flow`, `flow id`, `startSignIn`, `rate limit`.
- Enumerated **every** `refs/remotes/up/*` branch (100+) and checked:
  - whether any contains `components/{oauth,google,apple,github}/cleanup.ts` → **none**;
  - whether any adds `by_expiresAt` to the OAuth tables → **none**;
  - whether any implements keyed flows (`flowId`, `pendingFlows`) in `methods/oauth` → **none**;
  - whether any changes `email/validation.ts` to do IDNA/Punycode (`domainToASCII`, `xn--`) → **none**.

> A GitHub timeline event on #30 references commit `272ef94b…` (ShintoTuna, 2026-05-03). That commit is no longer fetchable from the repository and ShintoTuna has **no** PRs in this repo, so there is no live overlap — but list it as a since-deleted attempt in your comment if you want to be thorough.

### 4.2 Per-candidate audit

| Candidate | PRs / commits / branches checked | Finding | Confidence |
|---|---|---|---|
| **#30 / OAuth doc cleanup** | Search `authorizationRequests`, `oauth cleanup`, `cleanup`, `crons`; branches for `cleanup.ts` and `by_expiresAt`; `git log --grep=cleanup`; issue timeline | Only hits are the **email** (#539) and **passkey** cleanup, and dowski's **session** sweeps (#785, #786, #799). No OAuth cleanup anywhere. PR #797 (WorkOS) touches the shared OAuth tables but adds no cleanup. #30 has 0 comments, 0 assignees, 0 linked PRs. | **Verified absent** |
| **Punycode email** | Search `punycode`; branches for `domainToASCII`/`xn--`; `git log --grep` | No implementing PR or branch. Only the TODO itself (introduced by #727) and its test case. | **Verified absent** |
| **Keyed pending flows** | Search `pending flow`, `keyed flow`, `flow id`; branch grep for `flowId`/`pendingFlows` | No PR or branch. `erquhart/oauth-flow-errors` only mentions "deferred cleanups" in an unrelated storage-error commit (2026-08-21). | **Verified absent** |
| **#581 WASM helper** | Search `581`, `wasm`, `argon2`, `convex-test`, `test helper`; timeline cross-references | Issue #581 is the **only** hit; zero cross-references; no PR. Underlying repo config predates the issue. | **Verified absent (and likely misdiagnosed)** |
| **#126 / #350 SSR adapter** | Search `tanstack`; issue timelines; #796 references both; branches `*ssr*`, `*nextjs*` | v2 shipped framework-agnostic primitives (`@convex-dev/auth/ssr`: `httpCookies`, `ServerAuthSession`, `setupConvexAuthServer`, handlers). No TanStack example. `PrathamRanka` asked to be assigned to #350 on 2026-06-09; **no maintainer reply, no assignee, no PR**. #126 has 6 comments, last 2026-03-17. | **Partially done; unclaimed** |
| **#59 / #755 sessions API** | Search `invalidateSessions`, `deleteUser`; issue timeline | #59 cross-references #755. No PR. v2 has component-level revocation but no public app-level helper. | **Open; needs API decision** |
| **#796 Better Auth migration** | All open PRs; branch `dowski/convex-auth-v2-migration-step1` | Draft PR [#802](https://github.com/convex/convex-auth/pull/802) (Nicolapps, 2026-11-05) adds scrypt verification for the v1→v2 hash migration; [#803–#806](https://github.com/convex/convex-auth/pull/803) rework password minimum length. | **In progress** |
| **Refresh-token sweep** | Open PRs #785, #786, #799; branch `dowski/expired-session-cleanup` | Actively implemented by dowski. | **In progress — do not touch** |
| **Rate limiting** | Search `rate limit`; source | Password `verifyPassword` and email challenge starts/lookups already use `@convex-dev/rate-limiter`. Username, core `signIn`/`signUp`/`refresh`/`revokeSessions`, anonymous, and OAuth `startSignIn` have **no** limiter. | **Partially done; broad** |
| **React Native schemes** | Search `custom scheme`, `React Native`; source | `allowedRedirectOrigins` still requires http(s) origins ([`lib/oauth/redemption.ts:65-95`](https://github.com/convex/convex-auth/blob/a7bdf81d2eb8c63b9bf4d7a78e30b2402f07ea40/packages/core/src/lib/oauth/redemption.ts#L65-L95)). No PR. | **Open, design needed** |

---

## 5. Best 3 contributions to tackle first

### 5.1 (Recommended) [#30](https://github.com/convex/convex-auth/issues/30) — OAuth authorization-request and ticket cleanup

**Goal:** no OAuth row survives past its `expiresAt` unless it is claimed first.

**Files (at `a7bdf81d`):**

| File | Change |
|---|---|
| `packages/core/src/lib/oauth/schema.ts` | Add `.index("by_expiresAt", ["expiresAt"])` to `authorizationRequestsTable` and `ticketsTable` (additive schema change). |
| `packages/core/src/components/oauth/schema.ts` | Add the same index to the two tables it defines inline. |
| `packages/core/src/components/{oauth,google,apple,github}/cleanup.ts` (new) | Mirror [`email/cleanup.ts`](https://github.com/convex/convex-auth/blob/reboot/packages/core/src/components/email/cleanup.ts): `WORKER_NAME`, `schedule*Cleanup(ctx)` via `ping(components.batchWorker, …)`, bounded `getExpired…` query using `by_expiresAt` (`gte(cursor)` + `lte(now)`), `deleteExpired…` internal mutation. Two loops: requests (10 min TTL) and tickets (2 min TTL). |
| `packages/core/src/components/{oauth,google,apple,github}/convex.config.ts` | `import batchWorker from "@convex-dev/batch-worker/convex.config.js"; component.use(batchWorker);` (same as passkey/email). |
| `packages/core/src/lib/oauth/providerFunctions.ts` | Accept an optional `scheduleCleanup: { request(ctx); ticket(ctx) }` and call it right after `insertAuthorizationRequest` / `insertTicket`. |
| `packages/core/src/components/{oauth,google,apple,github}/provider.ts` | Pass the component's own schedulers (custom `oauth` component edits its four handlers directly). |
| `packages/core/src/testing/{oauth,google,apple,github}.ts` | Register the batch worker in the test helpers (`register as registerBatchWorker` from `@convex-dev/batch-worker/test`), as [`emailTestSetup.ts`](https://github.com/convex/convex-auth/blob/reboot/packages/core/src/components/emailTestSetup.ts) does. |

**Tests:**
- New `cleanup.test.ts` per component (or one shared contract test invoked four times), copied in structure from `email/cleanup.test.ts`: empty table → `idle`; expired batch deleted; live row → `timeoutMs` equal to its remaining TTL; cursor advances; a row exactly at `expiresAt` matches the claim semantics (claim uses `expiresAt < Date.now()`, so the cleanup boundary must use the same `<`, not `<=`).
- Existing `provider.test.ts` suites must keep passing; they glob `./**/*.ts`, so the new modules are picked up automatically.
- Run: `pnpm codegen && pnpm test && pnpm lint && pnpm typecheck && pnpm check:declarations` (CI also runs `format:check`, `check:doc-examples`, and a docs build).

**Scope boundary:** do **not** also try to authenticate/rate-limit `startSignIn` in this PR. That is a separate design decision (which component mounts the limiter, what key, what limits). Mention it as follow-up in the PR description.

**Why it is likely accepted:** it advances a maintainer-authored `enhancement` issue, is literally on the pre-GA known-issues list, copies two in-tree patterns, and changes no public API.

---

### 5.2 Punycode / internationalized email domains

**Goal:** accept `a@exämple.com` by canonicalising the domain to `a@xn--exmple-cua.com`, without allowing what Resend rejects.

**Design decision to settle in the PR:** canonicalise **before storing and sending**, so the row's `email`, `normalizedEmail`, and the Resend recipient all agree. The WHATWG `URL` parser performs IDNA ToASCII in Convex's runtime, so no new dependency is needed: `new URL("http://exämple.com").hostname === "xn--exmple-cua.com"`. (Do **not** import `node:url`'s `domainToASCII`; components run in the default/edge runtime.)

**Files:**
- [`packages/core/src/components/email/validation.ts`](https://github.com/convex/convex-auth/blob/a7bdf81d2eb8c63b9bf4d7a78e30b2402f07ea40/packages/core/src/components/email/validation.ts): split local/domain; keep the local part printable-ASCII (SMTPUTF8 is out of scope and Resend rejects it); IDNA-encode the domain; re-apply the dot/ASCII/IP-literal checks. Export a `canonicalizeEmail` (or extend `normalizeEmail`) that lowercases and punycodes.
- The `start`/`startChangeEmail` handlers in `components/email/challenge/*.ts` and `methods/email-password/server.ts`: run the canonical form through validation, storage, and the email sender.
- [`packages/core/src/components/email/validation.test.ts`](https://github.com/convex/convex-auth/blob/a7bdf81d2eb8c63b9bf4d7a78e30b2402f07ea40/packages/core/src/components/email/validation.test.ts): move the non-ASCII-domain case from reject → accept; assert the exact punycode output; keep non-ASCII local parts, IP literals, and control characters rejected; add a malformed-IDN case.
- `packages/docs/docs/login-providers/email-password.mdx`: one sentence on IDN support.

**Why:** maintainer-authored TODO from three weeks ago, tiny surface, pure unit-testable logic, real gap for non-Latin users. Lowest acceptance risk of the three.

---

### 5.3 Keyed pending OAuth flows (ask first)

**Goal:** two concurrent sign-ins in different tabs both complete.

**Server:**
- Add a non-secret `flowId` to `authorizationRequestFields` (`lib/oauth/schema.ts`) and to the custom oauth schema; mint it in `buildStartSignIn`.
- Return `{ redirect, state, flowId }` from `startSignIn`.
- Append `flowId` to the callback redirect in `redirectToApp` (never the `state`), and strip it on completion.

**Client** ([`methods/oauth/client.ts`](https://github.com/convex/convex-auth/blob/a7bdf81d2eb8c63b9bf4d7a78e30b2402f07ea40/packages/core/src/methods/oauth/client.ts)):
- Store under `` `${OAUTH_FLOW_STORAGE_KEY}:${flowId}` ``; `takePendingFlow(storage, flowId)`; `handleCallback` reads `flow` from the URL, takes only that entry, and removes only that entry.
- Keep the invariant from `KNOWN_ISSUES.md`: **the `state` is never read from the URL**, only the storage entry it selects. A missing/unknown `flowId` must still return `INVALID_FLOW`, and an error callback must clear the matching entry only.

**Tests:** `methods/oauth/client.test.ts` — two flows in one storage; finishing flow A leaves B intact; wrong `flowId` → `INVALID_FLOW`; `flow` param stripped; error callback clears the right entry. This is the one candidate where I would post a design comment **before** writing code.

---

## 6. External contribution policy — evidence

### 6.1 What the repo says

| Artefact | Finding |
|---|---|
| [`CONTRIBUTING.md`](https://github.com/convex/convex-auth/blob/reboot/CONTRIBUTING.md) | A **development guide only** (`pnpm install`, build, test, release). It never mentions pull requests, external contributors, a CLA, or a review process. |
| `README.md` | Points v1 → `main`, v2 → `reboot`. No contribution section. |
| `.github/` | Workflows only. **No** `PULL_REQUEST_TEMPLATE.md`, **no** `ISSUE_TEMPLATE/`, **no** `CODEOWNERS`. |
| `LICENSE` | **No license file**; GitHub API reports `"license": null`. No CLA or DCO text (`grep -i "contributor license\|CLA"` → nothing). |
| `AGENTS.md` | Detailed architecture/build rules, useful for crafting a PR that passes CI, but not a contribution policy. |
| Issue guidance | None. `enhancement` / `major` / `bug` / `documentation` / `needs feedback` labels exist but are applied sparsely. No issue is assigned. |

### 6.2 What has actually happened

**For (historically accepted):**

- Non-Convex PRs merged on `main`/v1: [#320](https://github.com/convex/convex-auth/pull/320) (eden881, 2026-06-08), [#336](https://github.com/convex/convex-auth/pull/336) and [#326](https://github.com/convex/convex-auth/pull/326) (Hades32), [#277](https://github.com/convex/convex-auth/pull/277) (nyoung697), [#244](https://github.com/convex/convex-auth/pull/244), [#247](https://github.com/convex/convex-auth/pull/247), [#239](https://github.com/convex/convex-auth/pull/239), [#234](https://github.com/convex/convex-auth/pull/234), [#149](https://github.com/convex/convex-auth/pull/149), and several docs fixes.
- Maintainers do occasionally answer external contributors (e.g. erquhart on [#350](https://github.com/convex/convex-auth/issues/350), dowski on [#73](https://github.com/convex/convex-auth/issues/73)).

**Against / cautious:**

- **292 PRs merged since 2026-06-25; 0 by non-Convex authors.** The most recent external merge is #320 on 2026-06-08, *before* v2 branch work began.
- Open external PR [#797](https://github.com/convex/convex-auth/pull/797) (WorkOS, created 2026-10-31) is a draft, `mergeStateStatus: DIRTY`, with **0 reviews** and no maintainer comment after 5 days.
- External PRs targeting `main` are stale: [#322](https://github.com/convex/convex-auth/pull/322) (April 2026, last touched June), [#468](https://github.com/convex/convex-auth/pull/468) (August 2026), [#160](https://github.com/convex/convex-auth/pull/160) (January 2025).
- External work is sometimes **re-landed** rather than merged: [`focus-stefano`'s #280](https://github.com/convex/convex-auth/pull/280) and [`Hades32`'s #289](https://github.com/convex/convex-auth/pull/289) were closed, and equivalent maintainer PRs [#296](https://github.com/convex/convex-auth/pull/296)/[#298](https://github.com/convex/convex-auth/pull/298) landed instead. Acceptance can happen without your PR being the merge commit — another reason to keep the diff small and the intent easy to cherry-pick.
- Maintainers do not triage issues: Nicolapps 0 comments, dowski 5 (v1-era), erquhart 23 (mostly v1 support). PRs are the medium of record.

**Verdict:** external PRs are **permitted in principle** (proven on `main`) and `reboot` is a normal, actively-targeted base (all maintainer PRs use it; #797 targets it). But **no external PR has yet been merged into v2**, and there is no written policy, license, or CLA. Treat v2 acceptance as **UNVERIFIED until a maintainer responds**. A short ask-first comment (§7) is the rational move for a multi-file change; a tiny docs/unit-test PR can reasonably go straight to draft.

### 6.3 Practical contribution mechanics

- **Base your PR on `reboot`**, not `main`. The repo default is `main` (v1), which will silently give you the wrong codebase.
- CI (`.github/workflows/typescript.yml`) runs: `pnpm install --frozen-lockfile`, `pnpm build`, `pnpm check:declarations`, `pnpm check:doc-examples`, `pnpm lint`, `pnpm format:check`, `pnpm typecheck`, `pnpm test`, and a docs build. Rust is only needed for `argon2id-wasm`.
- `pnpm codegen` must be run when component schemas/config change (it rewrites `_generated/api.ts` and friends); CI does not do it for you, and a stale generated file will fail review.
- File-naming rule from `AGENTS.md`: two dots (`.test.ts`, `.fixture.ts`) means "not a Convex module"; use `.fixture.ts` for test-only modules inside a component directory.
- Compile rules: relative imports in `packages/core/src` carry the on-disk extension (`./client.ts`), because of `moduleResolution: NodeNext` + `rewriteRelativeImportExtensions`.

---

## 7. Suggested GitHub comment

This one goes on **issue #30**, which exists, is maintainer-authored, and is unclaimed. It references the maintainer-authored known issue, narrows scope, states the boundary, and offers a draft PR.

> Hi — I'd like to pick up the stale-data cleanup for OAuth, as the remaining slice of this issue. In v2, expired verification/challenge rows are already swept (`components/email/cleanup.ts`, `components/passkey/cleanup.ts`) and session sweeping is in progress (#785/#799), but `authorizationRequests` and `tickets` are still only deleted when their secret is later presented (`packages/core/src/lib/oauth/dbHelpers.ts`), which `KNOWN_ISSUES.md` calls out explicitly.
>
> Proposed scope: add a `@convex-dev/batch-worker` loop to each OAuth component (`oauth`, `google`, `apple`, `github`), mirroring `components/email/cleanup.ts` — a `by_expiresAt` index on both tables, a bounded `getExpired*` query and a delete mutation — scheduled from `createAuthorizationRequest` and `createTicket`. I'd add cleanup tests in the style of `email/cleanup.test.ts` and register the batch worker in the `testing/*` helpers.
>
> I'd deliberately leave the "`startSignIn` is unauthenticated" half out of this PR, since rate limiting needs a decision about which component owns the limiter and what the limits are. That split is also how `KNOWN_ISSUES.md` frames it.
>
> I checked the open and closed PRs and the `up/*` branches and didn't find existing work on the OAuth cleanup (I did see a since-deleted commit from May that referenced this issue). Does this direction work for you, or is someone already on it? Happy to open a draft PR first if you'd rather review the shape before I polish it.

*Why this wording works:* it proves you read the source, ties the work to a maintainer-authored issue and a maintainer-authored known-issues entry, narrows scope, mirrors an accepted pattern, explicitly avoids the contentious half, and gives an easy "yes / someone's on it" reply.

---

## 8. Final recommendation

**Work on [#30](https://github.com/convex/convex-auth/issues/30), scoped to OAuth authorization-request and ticket cleanup.**

Reasoning, in order:

1. **It is a real maintainer-opened issue** — by Convex co-founder Michal Srb (`xixixao`), labelled `enhancement`, still open, zero comments, zero assignees. This satisfies the brief's preference, unlike anything in the v2-era tracker (which has none).
2. **Its scope has been explicitly consolidated by a current maintainer.** erquhart closed #17 as *"Superseded by #30, which covers this along with other stale data cleanup."*
3. **The remaining v2 slice is precisely defined.** Email and passkey cleanup shipped; sessions are in active PRs; OAuth is the only stale-data class with nothing — and `KNOWN_ISSUES.md` §2 documents it as a pre-GA item.
4. **It is unclaimed, and I verified that beyond GitHub's PR links.** No open/closed PR, no commit, no `cleanup.ts`, no `by_expiresAt`, no branch among 100+ upstream refs.
5. **It is a real production problem,** not polish: unbounded table growth from ordinary abandoned logins, amplified by an unauthenticated public `startSignIn` that anyone can spam.
6. **The design is already settled by precedent.** `email/cleanup.ts` and `passkey/cleanup.ts` give an exact template — batch-worker `ping`, bounded range query, cursor semantics, test structure. There is very little to argue about.
7. **It fits your stack.** TypeScript, Convex components, schema/indexes, `convex-test`, Vitest — no Rust, no React internals, no browser security model.
8. **Scope is controllable.** Four small components + one shared helper + tests; the contentious `startSignIn` authentication is explicitly deferred.

**Fallback if you want a warm-up first:** the Punycode/IDN email TODO (§5.2). It is ~10× smaller, also maintainer-authored (Nicolapps), and a clean first-PR signal. Doing it first and the OAuth cleanup second is a defensible sequence.

**Do not** start with #581 (likely a consumer-config problem already solved in-repo), #796 (active draft PRs), the refresh-token sweep (dowski is on it), #126/#350 (needs an example + guide design), or any of the v1 OAuth issues in §3.

---

## Appendix A — reproducibility notes

Raw data cached during research (local paths, not part of the repo):

- `/tmp/opencode/issues_all.json` — 177 issues (all states)
- `/tmp/opencode/prs_merged.json` — 422 merged PRs
- `/tmp/opencode/prs_closed.json` — 519 closed-unmerged PRs
- `/tmp/opencode/prs_all.json` — 300 most recent PRs (76 open)
- `/tmp/opencode/reboot` — detached worktree at `a7bdf81d`

Useful commands:

```sh
gh issue list --repo convex/convex-auth --state all --limit 500 \
  --json number,title,author,createdAt,state,labels,assignees,url
gh pr list --repo convex/convex-auth --state merged --limit 1000 \
  --json number,author,mergedAt,baseRefName,title,url
gh api -X GET search/issues -f q='repo:convex/convex-auth is:pr cleanup'
git -C <reboot> log --all --grep=punycode -i
git -C <reboot> branch -r --contains <sha>
```

## Appendix B — items labelled UNVERIFIED

| Claim | Status |
|---|---|
| `erquhart` is a current Convex employee | Strong evidence (bio mentions `@get-convex`; owns `KNOWN_ISSUES.md` and OAuth/SSR code; 37 merged PRs) but **not** confirmed via org-membership API (requires org admin). |
| `sshader` is a Convex co-founder | Public knowledge; GitHub profile has no company field. Historical only on this repo. |
| `xixixao` (Michal Srb) is a Convex co-founder | Public knowledge; GitHub profile company is `@get-convex`. His authorship of #30 is independently verified via the issue API, so the recommendation does not depend on the title. |
| #363 still reproduces in v2 | Not tested. v2 replaced the client and wraps refresh in `retryOnNetworkError`; labelled as likely obsolete, not proven. |
| Whether a maintainer is privately planning the OAuth cleanup | Cannot be known from public data. The ask-first comment in §7 mitigates this. |
| Whether #797 (WorkOS) will be accepted/merged | Open draft, dirty merge state, 0 reviews at time of writing. |
| The `272ef94b…` commit that referenced #30 | No longer fetchable; author has no PRs. Treated as a deleted attempt, not live overlap. |
