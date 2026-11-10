# PromiseProof — Judge Installation & Reproducible Test

**Applies to:** PromiseProof — Commitment Impact, Forge production v2.2.0 (last observed November 10, 2026), read-only release  
**Products required:** Jira Cloud **and** Confluence Cloud on the **same Atlassian site**  
**Audience:** A site administrator installing the app; an ordinary Jira/Confluence user trying the workflow  
**Publisher:** Independent developer, [ShenJun93](https://github.com/ShenJun93)

## What you're testing

A delivery promise is written in Confluence, but its underlying Jira work can move without changing the promise. PromiseProof lets an authorized user **attest** a specific published promise, compare it with **live Jira source evidence**, and see the exact risk and next human action. It also supports temporary in-session snapshots, bounded Jira due-date history, and **read-only** what-if scenarios.

**Important scope:** The app checks **only the sources you select**. It does not guarantee delivery, invent dependencies, edit issues, publish Confluence pages, or claim that inaccessible sources are on track.

## 1. Install as a non-contributor site admin

1. Use the **official Atlassian installation link supplied with the Codegeist submission** (not the in-app Jira deep link). It should open an Atlassian Developer Console install page for `promiseproof-codegeist`.
2. Use a Jira + Confluence Cloud test site **other than the publisher's demonstration site**. You must have permission to install apps on that site.
3. Install PromiseProof on **Jira** and also on **Confluence**, using the same installation link and the same site. Both installations are needed for the cross-product flow. If the page offers one product per installation, repeat for the second product.
4. Review the only requested scopes: `read:jira-work` and `read:page:confluence`. No Jira or Confluence write scope, KVS permission or external egress is needed by this version.
5. In Jira, open **Apps → PromiseProof — Commitment Impact** (or the installed Jira global page for the app). If the menu location differs, use Jira's installed-apps navigation.

The publisher's existing fixture IDs are **not portable**. Create your own synthetic page and Jira TEST issues. The quick smoke matches the example shown in the production app. The advanced change-history test is a separate fixture.

## 2. Quick smoke — create your own synthetic evidence

**Confluence:** Publish a regular page your test user can read, containing this exact standalone passage:

> Deliver demo release by 2027-02-15

Copy the actual page URL or numeric page ID. The published passage has **no final period**; paste exactly the same text into the app.

**Jira:** Create two ordinary TEST issues in an accessible project and set their native **Due date** fields:

| Issue (example only) | Due date | Expected comparison |
|---|---|---|
| `YOURKEY-1` | `2027-02-13` | Two days before the promise |
| `YOURKEY-2` | `2027-02-20` | **Five days after** the promise |

Use your site's real issue keys, never these placeholders. If the Due date field is missing from Create, ask the Jira administrator to expose it or set it on the issue edit screen. These are source-data changes made by a test user in Jira, **not by PromiseProof**.

## 3. Verify the quick smoke (expected: AT_RISK)

In **Jira → Apps → PromiseProof — Commitment Impact**, enter:

| Input | Value |
|---|---|
| Confluence page ID or page URL | Your actual published page |
| Human-confirmed deadline | `2027-02-15` |
| Exact commitment passage | `Deliver demo release by 2027-02-15` |
| Jira issue keys | Your two actual TEST keys |
| Commitment attestation | Confirm the passage is the intended delivery commitment |

Select **Verify selected sources**.

**Expected:** `AT_RISK / DATE_CONFLICT`; 1 of 2 selected issues is five calendar days later than the published promise. Follow the links to original Jira and Confluence sources. This checks **date alignment of selected work**, not actual release completion or acceptance.

**Fail-closed check:** Change only the passage **input in PromiseProof** to `This commitment does not exist in the published page`, without editing Confluence. Verify again. Expect `UNKNOWN / PASSAGE_UNVERIFIED`. Restore the exact published passage and re-Verify; the observed result returns to `AT_RISK`.

**Optional What-if:** Simulate moving the late issue's due date to `2027-02-15`. A hypothetical `ON_TRACK` outcome may appear, but the observed Jira due date must remain `2027-02-20`. PromiseProof does not perform that edit.

## 4. Advanced drift/history — separate initial fixture

If you want to demonstrate **ON_TRACK → AT_RISK** instead of starting with an already-late issue, use a **fresh pair of TEST issues** and the same published promise/date (`2027-02-15`).

1. Set both initial Jira Due dates to `2027-02-12` and `2027-02-13`. Verify `ON_TRACK`, then select **Pin current verified snapshot** in the same app session.
2. **Outside PromiseProof**, an authorized Jira issue editor moves the first Due date from `2027-02-12` to `2027-02-20` (an eight-day extension).
3. Re-Verify without reloading the app. Expect a source-change indication and `AT_RISK / DATE_CONFLICT` with the moved issue now five days later than the promise.
4. Inspect bounded Jira due-date history if available. What-if remains separate from observed source changes.

Do not mix this advanced fixture's **initial dates** with the Quick Smoke pair above. A new or permission-limited Jira issue may expose only partial history.

**Permission safety:** When a source is inaccessible to the signed-in test user, the app must return `UNKNOWN` rather than a fabricated positive verdict. Source access follows Atlassian permissions. Do not post private customer or tenant data in support issues.

## 5. Reviewer acceptance checklist

- [ ] Installed successfully as a **non-contributor admin** on a separate Jira + Confluence Cloud site
- [ ] Both Jira and Confluence installations are present
- [ ] Read-only permissions only
- [ ] Published page and two actual Jira issue keys were read with ordinary user access
- [ ] `AT_RISK` evidence and later due date were correct
- [ ] Advanced fixture: Pin → re-Verify after Jira change shows changed evidence
- [ ] Quick smoke → `AT_RISK` five-day gap; advanced test → eight-day Due date move
- [ ] What-if stayed **hypothetical**
- [ ] Unavailable exact passage → `UNKNOWN`
- [ ] Restricted-source permissions did not expose data or produce a false positive

Please report the site type (test/production), outcomes and non-sensitive screenshots in a [support issue](https://github.com/ShenJun93/promiseproof-codegeist-docs/issues). **Never post private Jira issue content, Confluence page text, credentials or tokens publicly.**

## Troubleshooting

| Symptom | Check |
|---|---|
| Cannot install | You must be a site admin. The site must run **both Jira and Confluence**. Use the **real distribution link** from the submission, not a Jira in-app URL. |
| Cannot locate PromiseProof | Verify the **Jira installation** and navigate to the Jira global-page entry under Apps. |
| `UNKNOWN` for the page | Confirm the page is published, the page ID is correct, the quoted passage is **exact**, and the signed-in user can read it. |
| `UNKNOWN` for a Jira issue | Use a real key (not `YOURKEY-1`), confirm the issue exists and the user can read it. |
| No timeline data | A fresh issue may have no due-date change history; make an authorized due-date edit in the advanced fixture, then re-Verify. Permissions and Jira history can limit what is visible. |
| Snapshot disappears on reload | By design: Pin is **in-session only**, not persistent server storage. |

## Privacy, support and limits

[Privacy Policy](./PRIVACY.md) · [Terms](./TERMS.md) · [Support](https://github.com/ShenJun93/promiseproof-codegeist-docs/issues)

This version is **not** a release approval, proof of delivery or compliance attestation. It does not persist commitment records using Forge KVS. The publisher may have access to application logs when Atlassian vendor log access is enabled; site administrators can inspect or disable that access. Read the [Privacy Policy](./PRIVACY.md) before installation.

PromiseProof is an independent project, not an official Atlassian product.