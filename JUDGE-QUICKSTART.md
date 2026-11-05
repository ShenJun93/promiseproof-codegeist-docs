# PromiseProof — Judge Installation & 8-Minute Test

**Applies to:** PromiseProof — Commitment Impact, Forge production v2.0.0, read-only release (November 2026)  
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

The publisher's existing fixture IDs are **not portable**. Please create the two test issues and Confluence page below.

## 2. Create a portable, reproducible test fixture

**Confluence:** Publish a regular page that your test user can read. Include the following **exact standalone sentence** in the published page body:

> Deliver Orion onboarding release by 2027-04-15

Copy the **numeric page ID** from the Confluence page URL. If the URL contains `/pages/123456789/`, enter `123456789` in PromiseProof.

**Jira:** In any accessible test project, create two ordinary issues. Set:

| Example issue | Due date | Meaning |
|---|---|---|
| `YOURKEY-1` | `2027-04-14` | Before the promise deadline |
| `YOURKEY-2` | `2027-04-19` | **4 days after** the promise deadline |

Use the **real issue keys on your site**, not the example keys. If due dates are missing from the Create form, add them using Jira's issue Edit screen, project configuration, or an authorized site administrator. Jira due dates are test-source changes made by the admin **outside** PromiseProof.

## 3. Verify the real evidence

In PromiseProof fill:

| Field | Value |
|---|---|
| **Confluence page ID or page URL** | Your actual published Confluence page ID |
| **Human-confirmed deadline (YYYY-MM-DD)** | `2027-04-15` |
| **Exact commitment passage from Confluence** | `Deliver Orion onboarding release by 2027-04-15` |
| **Jira issue keys (1–5, comma-separated)** | The two real test issue keys |
| **Commitment attestation** | Check **I confirm this passage is an intended delivery commitment** |

Choose **Verify selected sources**.

**Expected evidence:** `AT_RISK`, with **one of the two selected Jira due dates later than the attested promise**, and **4 days** of date exposure. The result should identify selected sources rather than fabricate a complete dependency graph. Follow the links to the underlying Jira and Confluence records.

If a user lacks permission to a selected source, the app must fail closed to `UNKNOWN` rather than claim the work is on track.

## 4. Demonstrate freshness, what-if and safe failure

- **Session snapshot:** Select **Pin current verified snapshot**. Without changing the real issues, select **Verify selected sources** again. The comparison should report `UNCHANGED`.
- **Real source change:** The *authorized Jira test issue editor*, outside the PromiseProof app, changes the second issue's due date from `2027-04-19` to `2027-04-21`. Verify again. The observed date exposure should now be **6 days**. A pinned prior observation should distinguish this changed source from the original snapshot. Read-only timeline/history is available for due-date changes when the user's Jira permissions and source history allow it.
- **Hypothetical scenario:** Explore read-only What-if and simulate bringing the later issue's due date on or before `2027-04-15`. The *simulated* outcome can improve while the actual observed Jira result remains `AT_RISK`. What-if **must not alter Jira**.
- **Fail-closed:** Replace the exact Confluence passage input with `This commitment does not exist in the published page` (do not edit the real Confluence page). Verify. Expect `UNKNOWN`, restoration guidance and no retained positive decision tools. Restore the exact published passage and verify again.
- **Permission check:** With a different ordinary test user who lacks access to the selected page or issue, verify that PromiseProof does not expose the restricted source's data or fabricate a positive verdict.

Optional cleanup: restore the synthetic Jira issue due date. Jira's historical changelog is not erased by reverting a field.

## 5. Reviewer acceptance checklist

- [ ] Installed successfully as a **non-contributor admin** on a separate Jira + Confluence Cloud site
- [ ] Both Jira and Confluence installations are present
- [ ] Read-only permissions only
- [ ] Published page and two actual Jira issue keys were read with ordinary user access
- [ ] `AT_RISK` evidence and later due date were correct
- [ ] Session Pin → re-Verify `UNCHANGED`
- [ ] Authorized Jira date edit → live re-Verify reflects the change
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
| No timeline data | A fresh issue may have no due-date change history; make an authorized due-date edit, then re-Verify. Permissions and Jira history can limit what is visible. |
| Snapshot disappears on reload | By design: Pin is **in-session only**, not persistent server storage. |

## Privacy, support and limits

[Privacy Policy](./PRIVACY.md) · [Terms](./TERMS.md) · [Support](https://github.com/ShenJun93/promiseproof-codegeist-docs/issues)

This version is **not** a release approval, proof of delivery or compliance attestation. It does not persist commitment records using Forge KVS. The publisher may have access to application logs when Atlassian vendor log access is enabled; site administrators can inspect or disable that access. Read the [Privacy Policy](./PRIVACY.md) before installation.

PromiseProof is an independent project, not an official Atlassian product.
