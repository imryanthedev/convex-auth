# Convex Auth v2: contribution opportunities

Research date: **2026-11-05**. Repo: <https://github.com/convex/convex-auth>. It is also reachable as `get-convex/convex-auth` (the org was renamed).
`reboot` head at research time: [`a7bdf81d`](https://github.com/convex/convex-auth/commit/a7bdf81d2eb8c63b9bf4d7a78e30b2402f07ea40) (2026-11-04). Its CI is green.

Sources: GitHub API and `gh` (issues, 624 PRs, commits, branches), plus a local checkout of `reboot` with one test run. Anything I could not verify is labelled `UNVERIFIED`.

---

## 0. Headline findings (read this first)

1. **No open issue authored by a maintainer targets v2.**
   - I listed all 98 open issues. Every maintainer-authored one is v1-era, written in 2024–2025 (`xixixao`, `thomasballinger`, `ianmacartney`, and `Nicolapps` #282).
   - The v2 team does not use issues for planning. They work through PRs, and through [`KNOWN_ISSUES.md`](https://github.com/convex/convex-auth/blob/reboot/KNOWN_ISSUES.md) and TODO comments on `reboot`.
   - That file lists "consciously deferred limitations, most should be addressed prior to v2 release".
   - So the best "maintainer-authored work items" are the KNOWN_ISSUES entries. They have no issue number, which makes them **ASK FIRST**.
2. **`reboot` is crowded.**
   - There are 345 PRs based on `reboot`. `Nicolapps` has 33 open, mostly drafts. `dowski` has 5 open plus a TOTP and "requirements" PR stack. `erquhart` has 2 open.
   - The easy wins (docs, small fixes) are mostly already claimed. The audit in section 3 shows what is genuinely unclaimed.
3. **External PRs are welcome on v1 and unproven on v2.**
   - Many external PRs have been merged to `main`. None has been merged to `reboot`. See section 5.
4. **Several open issues that look like v2 work are already done or do not apply to v2.**
   - #755 is implemented on `reboot`. #674 does not apply to v2.
   - Details are in section 2.

---

## 1. Maintainer list

GitHub's collaborator-permission endpoint returns 403 without push access, so I could not read roles directly. These roles are inferred from public evidence.

| User | Role | Evidence |
|---|---|---|
| [`Nicolapps`](https://github.com/Nicolapps) | **Convex employee, primary v2 maintainer** | Profile org is `@get-convex`. 219 of the last ~800 `reboot` commits, the most recent being [#800](https://github.com/convex/convex-auth/pull/800) and [#722](https://github.com/convex/convex-auth/pull/722). 202 merged and 33 open `reboot` PRs. |
| [`dowski`](https://github.com/dowski) | **Core maintainer (sessions, TOTP, docs site)** | 95 `reboot` commits, including [#757](https://github.com/convex/convex-auth/pull/757) stateful sessions, [#759](https://github.com/convex/convex-auth/pull/759) revocation, [#798](https://github.com/convex/convex-auth/pull/798) TTL split, and [#790](https://github.com/convex/convex-auth/pull/790) Docusaurus. His profile shows no company, so his employment is `UNVERIFIED`. His role is clear from his authority over core merges. |
| [`erquhart`](https://github.com/erquhart) | **Convex-affiliated maintainer (OAuth, SSR)** | Bio says "@get-convex". 60 `reboot` commits and 16 merged `reboot` PRs. Owns the OAuth component and SSR handlers; TODOs are tagged `TODO(erquhart)`. |
| [`xixixao`](https://github.com/xixixao) | **Convex employee, v1 author** | Profile shows `@get-convex`. 318 commits overall, and authored the v1-era issues (#1–#59). Not active on `reboot` PRs in the 2026 data I pulled. |
| [`sshader`](https://github.com/sshader) | **Convex employee, v1** | 81 commits, a past maintainer. No recent activity seen. |
| [`thomasballinger`](https://github.com/thomasballinger) | **Convex employee** | Bio says "…at Convex". 25 commits. Authored #126, #179, #180. |
| [`ianmacartney`](https://github.com/ianmacartney) | **Convex employee** | Profile company is "Convex". Authored #54 and #176. Recent draft PRs [#508](https://github.com/convex/convex-auth/pull/508) and [#509](https://github.com/convex/convex-auth/pull/509). |
| [`reeceyang`](https://github.com/reeceyang) | Convex-affiliated (`@get-convex`) | Only one PR, an exploratory draft ([#778](https://github.com/convex/convex-auth/pull/778), titled "DO NOT REVIEW"). Not a maintainer of this repo. |
| [`sethconvex`](https://github.com/sethconvex) | **Unclear, `UNVERIFIED`** | Empty profile. Opened `reboot` and `v2-preview` PRs [#751](https://github.com/convex/convex-auth/pull/751), [#675](https://github.com/convex/convex-auth/pull/675), [#752](https://github.com/convex/convex-auth/pull/752) (all self-labelled "AI slop, WIP") and the v1 PR #352. The handle suggests a Convex link, which I could not confirm. |
| [`magicseth`](https://github.com/magicseth) | `UNVERIFIED` | Pushed branches `magicseth/auth-v2-*`, but has no commits in the `reboot` log I sampled. |

**Not maintainers:** `robelest` is external (Trestle, [#797](https://github.com/convex/convex-auth/pull/797) WorkOS draft). `renovate[bot]` and `dependabot[bot]` are bots. The one-off contributors (`Hades32`, `goffrie`, `eden881`, `CodeZeno`, etc.) are outside the core team. One caveat: `goffrie` ([#444](https://github.com/convex/convex-auth/pull/444), `api.convex.dev` URL) looks like a Convex backend engineer, `UNVERIFIED`.

---

## 2. Top 10 candidates

The table is ordered by overall value to you, not by author. Section 7 gives the final pick.

| # | Item | Author / source | Date | Classification | Priority | Complexity |
|---|---|---|---|---|---|---|
| 1 | [#581](https://github.com/convex/convex-auth/issues/581) Password test helper can't load Argon2 WASM in `convex-test` | `nabilfatih` (external) | 2026-08-30 | **ASK FIRST** (bug verified, fix design needs approval) | High | Low–Medium |
| 2 | [KNOWN_ISSUES](https://github.com/convex/convex-auth/blob/reboot/KNOWN_ISSUES.md): OAuth component documents never cleaned up | Maintainers (no issue) | 2026-10-15 | **ASK FIRST** | High | Medium |
| 3 | [KNOWN_ISSUES](https://github.com/convex/convex-auth/blob/reboot/KNOWN_ISSUES.md): one pending OAuth flow per storage | Maintainers (no issue) | 2026-10-15 | **ASK FIRST** (touches security design) | Medium | Medium–High |
| 4 | [#30](https://github.com/convex/convex-auth/issues/30) Add crons for cleaning up stale data | `xixixao` (2024-07-11) | open | **ALREADY IN PROGRESS** for sessions ([#785](https://github.com/convex/convex-auth/pull/785), [#799](https://github.com/convex/convex-auth/pull/799)). Passkey and email cleanup are merged. The OAuth gap is item 2. | – | – |
| 5 | [#176](https://github.com/convex/convex-auth/issues/176) / TODO: let apps customize email templates and localize | `ianmacartney` (2025-03-09) | open | **ASK FIRST** (overlaps `Nicolapps` authEmail work, [#701](https://github.com/convex/convex-auth/pull/701)/[#702](https://github.com/convex/convex-auth/pull/702)/[#703](https://github.com/convex/convex-auth/pull/703)) | Medium | Medium |
| 6 | [#126](https://github.com/convex/convex-auth/issues/126) TanStack Start support, plus [#350](https://github.com/convex/convex-auth/issues/350) and [#796](https://github.com/convex/convex-auth/issues/796) | `thomasballinger` (2024-11-26) | open | **ASK FIRST** (large; the v2 core SSR layer is framework-agnostic, but an adapter or example needs design buy-in) | Medium | High |
| 7 | KNOWN_ISSUES: rate limiting on public routes | Maintainers | 2026-10-15 | **ASK FIRST** (security-sensitive, large) | High | High |
| 8 | TODO: derive `PROVIDER_NAME` from the mount path (4 `methods/*/server.ts` files) | Maintainers (code TODO) | – | **ASK FIRST** (overlaps rename PRs [#749](https://github.com/convex/convex-auth/pull/749)/[#750](https://github.com/convex/convex-auth/pull/750)) | Low | Low |
| 9 | [#755](https://github.com/convex/convex-auth/issues/755) `invalidateSessions` from a mutation, and [#59](https://github.com/convex/convex-auth/issues/59) | `saibotma` / `xixixao` | 2026-10-18 | **NOT RELEVANT TO V2**: v2 already has `revokeSessions` and `revokeOtherSessions` ([#759](https://github.com/convex/convex-auth/pull/759), [#775](https://github.com/convex/convex-auth/pull/775), [#779](https://github.com/convex/convex-auth/pull/779)) | – | – |
| 10 | [#674](https://github.com/convex/convex-auth/issues/674) JWKS `max-age=15` | `davidoort` | 2026-10-03 | **NOT RELEVANT TO V2**: v2 uses deployment-issued JWTs ([#787](https://github.com/convex/convex-auth/pull/787)). JWKS is served by Convex at `${CONVEX_CLOUD_URL}/.well-known/jwks.json`, not by this library. | – | – |

Other open issues I checked and discarded (all v1 code paths, citing `0.0.9x`):

- [#756](https://github.com/convex/convex-auth/issues/756), [#436](https://github.com/convex/convex-auth/issues/436), [#363](https://github.com/convex/convex-auth/issues/363), [#355](https://github.com/convex/convex-auth/issues/355) and similar. v2 has no provider-options merge and no `signIn.ts` Auth.js provider path.
- I did not test v2 behaviour for #363 (refresh over a failed network). Its status on `reboot` is `UNVERIFIED`; see [`browser/sessionManager.ts`](https://github.com/convex/convex-auth/blob/reboot/packages/core/src/browser/sessionManager.ts) and [`retry.ts`](https://github.com/convex/convex-auth/blob/reboot/packages/core/src/browser/retry.ts).
- OAuth provider bugs [#457](https://github.com/convex/convex-auth/issues/457), [#619](https://github.com/convex/convex-auth/issues/619), [#513](https://github.com/convex/convex-auth/issues/513), [#672](https://github.com/convex/convex-auth/issues/672). They concern the v1 provider code. #457 is self-described as AI-generated, and someone asked to be assigned to it.

### Notes on the highest-ranked items

**#581 (verified).**
- Running the `react-password` example test from the example directory fails with `Error: Cannot find package 'wbg' imported from …/argon2id-wasm/rust/pkg/argon2_wasm_bg.wasm` (18 of 20 tests fail). The error is identical to the reporter's.
- Running the same suite from the repo root passes 20/20. The root [`vitest.config.ts`](https://github.com/convex/convex-auth/blob/reboot/vitest.config.ts) installs a custom `wasmModulePlugin` that loads `.wasm` as a `WebAssembly.Module`. Its comment says "In production, the bundler used by the Convex CLI does this automatically."
- So the helper `registerPasswordProvider` ([`testing/password.ts`](https://github.com/convex/convex-auth/blob/reboot/packages/core/src/testing/password.ts)) only works if the consumer copies that undocumented plugin. The docs have no match for `wasm`, `convex-test` or `registerPassword`.
- The reporter's version (`2.0.0-alpha.1`) and import path (`providers/testing/password`) are old, but the underlying gap reproduces today. The maintainers have not responded; the issue has 0 comments.

**KNOWN_ISSUES OAuth cleanup.**
- Quote: "Expired authorization requests and tickets are only deleted when their secret is later presented, so abandoned flows accumulate forever."
- `components/passkey/cleanup.ts` and `components/email/cleanup.ts` ([#539](https://github.com/convex/convex-auth/pull/539)) are working templates built on `@convex-dev/batch-worker`. There is no `components/oauth/cleanup.ts`.
- `lib/oauth/schema.ts` already has `expiresAt` fields at lines 28 and 50.

---

## 3. PR overlap audit

Method:
1. Pulled all 624 PRs with titles, bodies, bases and states, and regex-searched titles and bodies, not only linked PRs.
2. Used `gh search prs` for `wbg OR argon2 OR wasm`.
3. Searched `git log up/reboot` by message.
4. Read the bodies of the PRs below.

I did **not** read every comment of every PR, so overlap with comment-only discussions is `UNVERIFIED`. The audit is a snapshot taken on 2026-11-05, and `Nicolapps` opened 5 new PRs on that day alone.

| Candidate | PRs / commits checked | Result |
|---|---|---|
| #581 test helper WASM | `gh search prs` for `wbg/argon2/wasm` returned nothing. `git log` for `argon2` and `wasm` only shows packaging commits ([#501](https://github.com/convex/convex-auth/pull/501), [#502](https://github.com/convex/convex-auth/pull/502), [#393](https://github.com/convex/convex-auth/pull/393)). Open [#802](https://github.com/convex/convex-auth/pull/802) (scrypt hashes) touches Argon2 but a different concern. No assignee. | **Verified: no PR addresses it.** [#802](https://github.com/convex/convex-auth/pull/802) may change hashing and should be watched. |
| OAuth doc cleanup | No OAuth-cleanup PR. [#411](https://github.com/convex/convex-auth/pull/411) (closed, original OAuth component), [#539](https://github.com/convex/convex-auth/pull/539) (merged, email only). [#785](https://github.com/convex/convex-auth/pull/785) and [#799](https://github.com/convex/convex-auth/pull/799) cover session and refresh-token cleanup only. | **No overlap found.** `erquhart` is working on neighbouring OAuth PRs, so coordinate. |
| Pending OAuth flows | Open OAuth PRs: [#744](https://github.com/convex/convex-auth/pull/744), [#746](https://github.com/convex/convex-auth/pull/746), [#715](https://github.com/convex/convex-auth/pull/715), [#742](https://github.com/convex/convex-auth/pull/742), [#751](https://github.com/convex/convex-auth/pull/751). None mentions keyed flows. | **No direct overlap found.** They edit the same client area (`methods/oauth/client.ts`), so expect merge conflicts. |
| Email templates | [#701](https://github.com/convex/convex-auth/pull/701), [#702](https://github.com/convex/convex-auth/pull/702), [#703](https://github.com/convex/convex-auth/pull/703) (convex sender, drafts), [#669](https://github.com/convex/convex-auth/pull/669)–[#671](https://github.com/convex/convex-auth/pull/671) (email address branding), [#408](https://github.com/convex/convex-auth/pull/408) (email validation WIP). | **Possible overlap** with `Nicolapps`. |
| Rate limiting | No PR found. | No PR, but a design decision. |
| TanStack / frameworks | [#718](https://github.com/convex/convex-auth/pull/718) (merged, auth.config.ts compiles without Node types, mentions TanStack). [#780](https://github.com/convex/convex-auth/pull/780) and [#789](https://github.com/convex/convex-auth/pull/789) by `erquhart` (Next.js provider and handshake, drafts), [#782](https://github.com/convex/convex-auth/pull/782) (closed, one SSR handler). | No TanStack adapter PR. SSR is `erquhart`'s area. |
| Session revocation (#755, #59) | [#759](https://github.com/convex/convex-auth/pull/759), [#775](https://github.com/convex/convex-auth/pull/775), [#779](https://github.com/convex/convex-auth/pull/779) (merged); open: [#786](https://github.com/convex/convex-auth/pull/786). `component/public.ts` has `revokeSessions`. | **Already implemented.** |
| WorkOS / enterprise SSO | [#797](https://github.com/convex/convex-auth/pull/797) (external, draft). | In progress by an external contributor. |
| TOTP / second factor | [#628](https://github.com/convex/convex-auth/pull/628), [#629](https://github.com/convex/convex-auth/pull/629)–[#634](https://github.com/convex/convex-auth/pull/634), [#652](https://github.com/convex/convex-auth/pull/652), [#666](https://github.com/convex/convex-auth/pull/666) and the `requirements-*` stack by `dowski`. | **Avoid.** |
| Docs gaps (JWKS, guides, migration) | About 20 open `Nicolapps` docs drafts ([#719](https://github.com/convex/convex-auth/pull/719), [#730](https://github.com/convex/convex-auth/pull/730), [#731](https://github.com/convex/convex-auth/pull/731), [#735](https://github.com/convex/convex-auth/pull/735)–[#741](https://github.com/convex/convex-auth/pull/741), [#745](https://github.com/convex/convex-auth/pull/745)). | **Avoid.** |
| Better Auth migration (#796) | No PR found. | Large; needs maintainer scoping. |

---

## 4. Best 3 contributions to tackle first

### 4.1 Make the password test helper work for consumers (#581)

**Goal.** An app using `convex-test` and `registerPasswordProvider` should work without hand-writing a Vite plugin.

**Ask the maintainers first.** There are two reasonable shapes:
- (a) Export the plugin, for example from `@convex-dev/auth/test` as `wasmModulePlugin`, and document it.
- (b) Do the wasm loading inside the test helper itself.
- A docs-only fix is the minimum fallback.

**Relevant files** (all on `reboot`):
- [`packages/core/src/testing/password.ts`](https://github.com/convex/convex-auth/blob/reboot/packages/core/src/testing/password.ts) (the helper; ships as `.ts` on purpose, see its header comment)
- [`vitest.config.ts`](https://github.com/convex/convex-auth/blob/reboot/vitest.config.ts) (`wasmModulePlugin`)
- [`packages/core/package.json`](https://github.com/convex/convex-auth/blob/reboot/packages/core/package.json) (`./components/password/test` export)
- [`examples/react-password/convex/password.test.ts`](https://github.com/convex/convex-auth/blob/reboot/examples/react-password/convex/password.test.ts)
- `packages/docs/docs/` (add a "Testing" page; none exists)

**Plan.**
1. Reproduce: from `examples/react-password`, `pnpm vitest run convex/password.test.ts` fails. From the repo root, `pnpm vitest run --project react-password` passes.
2. Move `wasmModulePlugin` into a published, tested helper.
3. Make the example's own `vite.config.ts` use it, so the example exercises exactly what consumers will.
4. Add a docs page for testing with `convex-test`.

**Tests.** Add a vitest config inside an example dir that does not inherit the root plugin and still passes. Run `pnpm build && pnpm lint && pnpm typecheck && pnpm test`, as `CONTRIBUTING.md` requires.

**Risk.** Medium, because [#802](https://github.com/convex/convex-auth/pull/802) may change the hashing path. Check its status before starting.

### 4.2 Clean up abandoned OAuth documents (KNOWN_ISSUES)

**Goal.** Expired authorization requests and tickets get erased by a background loop, like the passkey and email components.

**Relevant files.**
- Template: [`components/passkey/cleanup.ts`](https://github.com/convex/convex-auth/blob/reboot/packages/core/src/components/passkey/cleanup.ts), [`cleanup.test.ts`](https://github.com/convex/convex-auth/blob/reboot/packages/core/src/components/passkey/cleanup.test.ts), and [`email/cleanup.ts`](https://github.com/convex/convex-auth/blob/reboot/packages/core/src/components/email/cleanup.ts)
- [`lib/oauth/dbHelpers.ts`](https://github.com/convex/convex-auth/blob/reboot/packages/core/src/lib/oauth/dbHelpers.ts), [`lib/oauth/schema.ts`](https://github.com/convex/convex-auth/blob/reboot/packages/core/src/lib/oauth/schema.ts), `components/oauth/convex.config.ts` (mount `@convex-dev/batch-worker`)

**Plan.**
1. Add indexes on `expiresAt` if they are missing.
2. Write `oauth/cleanup.ts` with a `scheduleCleanup(ctx)` call from `startSignIn` and from ticket creation.
3. Mount the batch worker in the component config, and regenerate `_generated`.
4. Remove the corresponding KNOWN_ISSUES section.

**Tests.** Copy the structure of the passkey `cleanup.test.ts`: expired rows are erased, unexpired rows are kept, and the loop goes idle.

**Notes.**
- The email cleanup file carries a `FIXME` ("this file is very similar to `passkey/cleanup.ts`"). The maintainers may prefer a shared helper over a third copy, so ask.
- `startSignIn` being unauthenticated is raised in the same KNOWN_ISSUES entry, so scope the PR to cleanup only.

### 4.3 Keyed pending OAuth flows (KNOWN_ISSUES)

**Goal.** Two OAuth sign-ins in different tabs stop overwriting each other.

**Fix direction from KNOWN_ISSUES.** Keyed pending flows, selected by a non-secret flow id in the redirect URL. The state itself must never be read from the URL, to preserve the login-CSRF protection.

**Relevant files.**
- [`methods/oauth/client.ts`](https://github.com/convex/convex-auth/blob/reboot/packages/core/src/methods/oauth/client.ts) (single `flow` key)
- [`client.test.ts`](https://github.com/convex/convex-auth/blob/reboot/packages/core/src/methods/oauth/client.test.ts), `react.test.tsx`, `testFlow.ts`
- [`ssr/nextjs/oauth.test.tsx`](https://github.com/convex/convex-auth/blob/reboot/packages/core/src/ssr/nextjs/oauth.test.tsx)

**Plan.**
1. Generate a flow id in `signIn`.
2. Store pending flows under `flow:<id>`.
3. Include the id in `redirectTo`.
4. On startup, look up the flow by that id and fall back to the old behaviour.

**Tests.** Two concurrent flows both complete. A mismatched id fails with `invalid_flow`. A URL-supplied state is still rejected.

**Risk.** Security-sensitive design, and it overlaps in code with `erquhart`'s open OAuth PRs. Confirm the design before coding.

---

## 5. External contribution policy

| Question | Evidence |
|---|---|
| Is there a contribution guide? | [`CONTRIBUTING.md`](https://github.com/convex/convex-auth/blob/reboot/CONTRIBUTING.md) on `reboot` is a "Developing guide": install, run examples, and run `pnpm build`, `lint`, `typecheck`, `test`. It says nothing about who may contribute. `main` has no `CONTRIBUTING.md`. |
| PR template, issue templates, CODEOWNERS, CLA? | I found **none** on either branch. Only the 6 workflow files under [`.github/workflows`](https://github.com/convex/convex-auth/tree/reboot/.github/workflows). |
| License? | `packages/core/package.json` declares `Apache-2.0`. GitHub's API reports no detected license, because there is no `LICENSE` file at either root. |
| Do external contributors submit PRs? | Yes, many. On `main` (v1), external PRs merged include [#336](https://github.com/convex/convex-auth/pull/336) and [#326](https://github.com/convex/convex-auth/pull/326) (`Hades32`), [#277](https://github.com/convex/convex-auth/pull/277) (`nyoung697`), [#244](https://github.com/convex/convex-auth/pull/244) (`johncmunson`), [#239](https://github.com/convex/convex-auth/pull/239) (`dickermoshe`), [#234](https://github.com/convex/convex-auth/pull/234) (`tkejr`), [#320](https://github.com/convex/convex-auth/pull/320) (`eden881`), and more. |
| Any external PR merged on `reboot`? | **No.** Merged `reboot` PRs come only from `Nicolapps`, `dowski` and `erquhart`. |
| External PRs open on `reboot`? | [#797](https://github.com/convex/convex-auth/pull/797) (`robelest`, draft). It has no human comment, only a Vercel bot saying a Convex team member must authorize its deployment. Whether the maintainers will accept it is `UNVERIFIED`. |
| Are external PRs reviewed in a timely way? | Mixed. Several external PRs to `main` are still open after months ([#322](https://github.com/convex/convex-auth/pull/322), [#306](https://github.com/convex/convex-auth/pull/306), [#305](https://github.com/convex/convex-auth/pull/305), [#335](https://github.com/convex/convex-auth/pull/335)), though each did receive some review. The `main` branch is explicitly in maintenance mode: the [README banner](https://github.com/convex/convex-auth/blob/main/README.md) points to v2. |
| Do `reboot` PRs get accepted? | Yes for the team. The README says "This branch contains a WIP implementation of Convex Auth v2" and links CONTRIBUTING for how to develop. There is no statement about outside PRs. |
| Maintainer guidance on proposing changes? | **None found.** An issue responder on [#350](https://github.com/convex/convex-auth/issues/350) is another outsider offering to implement it. |

**Conclusion.**
- v2 is a WIP developed almost entirely by three staff members who write many small PRs.
- Nothing forbids an external PR, and the repo has accepted external code before. But I found **no recorded example of an external PR landing on `reboot`**, and no guidance. That is unverified territory.
- Open an issue or comment first (see section 6). Keep PRs small, and target `reboot`, not `main`.

---

## 6. Suggested GitHub comment

For [#581](https://github.com/convex/convex-auth/issues/581). Edit as you like before posting.

> Hi! I reproduced this on current `reboot` (`a7bdf81d`). Running `examples/react-password/convex/password.test.ts` from the example directory fails with `Cannot find package 'wbg' imported from …/argon2id-wasm/rust/pkg/argon2_wasm_bg.wasm`. Running it from the repo root passes, because the root `vitest.config.ts` has a `wasmModulePlugin` that consumers don't have.
>
> I'd like to fix this for v2 users. My proposal is to export that plugin (or an equivalent) from `@convex-dev/auth/test`, use it in the example's own Vite config, and add a short "Testing with convex-test" docs page. Would you prefer that, loading the wasm inside `registerPasswordProvider` itself, or documentation only? I'll wait for your preference before opening a PR against `reboot`. I also noticed #802 touches the password hashing; I'll check that first so we don't collide.

---

## 7. Final recommendation

**Start with [#581](https://github.com/convex/convex-auth/issues/581), after posting the comment in section 6.**

Why this one:
- **Real and reproducible on `reboot` today.** It is a documented consumer-facing gap, not stale v1 noise.
- **No overlap.** I found no PR for it, and the drafts in flight (docs, TOTP, OAuth, sessions) don't touch it.
- **Matches your stack.** It is TypeScript, Vite/Vitest and Convex, with no Rust or OAuth security design.
- **Small and testable.** The change is bounded (a helper, a config, a docs page) with an objective success test: the example suite passes from its own directory.
- **Good first PR.** A concrete, maintainer-visible fix on a thinly staffed area earns trust before you take on the OAuth items.

The risk is that no maintainer has commented on the issue. I'd therefore ask before coding.

**Second choice:** OAuth document cleanup (4.2). It is clearly wanted, and there is a close template (`passkey/cleanup.ts`). It sits in `erquhart`'s area, so ask first.

Do **not** start on TOTP, docs rewrites, email delivery, or Better Auth migration. They are either already claimed by the team or too large to be a first contribution.

### Verification caveats
- No issue was found that a maintainer authored for v2, so "AVAILABLE" is not used for anything. Everything is **ASK FIRST**, because no maintainer has asked for outside help on these.
- I confirmed #581 only locally, with one test run on Node 22, 24 and 26. I did not run the helper in an independent consumer project.
- I did not run the other candidates. Their status comes from reading the code and PR text.
- `Nicolapps` is opening several PRs per day, so re-run the overlap check just before you start.
