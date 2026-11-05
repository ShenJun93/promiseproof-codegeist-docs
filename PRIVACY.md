# PromiseProof — Privacy Policy

**Effective date:** November 5, 2026  
**App:** PromiseProof — Commitment Impact, an independent Forge app for Atlassian Jira and Confluence  
**Publisher:** Independent developer (GitHub: [ShenJun93](https://github.com/ShenJun93))  
**Contact:** [PromiseProof support and privacy requests](https://github.com/ShenJun93/promiseproof-codegeist-docs/issues)

## What the app does

PromiseProof helps an authorized user compare the wording and date of a delivery commitment on a selected Confluence page with due-date evidence from selected Jira issues. The user explicitly selects the source page, attests the commitment passage and deadline, and chooses one to five Jira issue keys. It presents source-linked, read-only observations, a temporary in-session comparison, and read-only “what-if” scenarios.

PromiseProof does **not** monitor all Jira work automatically, approve delivery, certify compliance, or modify Jira issues or Confluence pages.

## Information processed

When you use the app, Atlassian Forge invokes the Jira and Confluence APIs with the permissions of the signed-in user. Depending on your selection and access rights, the app can process:

- The selected Confluence page text, its version and related source metadata.
- Selected Jira issue keys, issue metadata, due dates and bounded due-date changelog details.
- Your manually entered commitment passage, deadline, issue selection and attestation.
- Session-only comparison and “what-if” inputs.

The current production version requests only **`read:jira-work`** and **`read:page:confluence`**. Access is subject to Atlassian's permissions. If a source cannot be checked, the app reports that the evidence is unknown rather than inventing a positive result.

## Storage and retention

**In the current publicly shared, read-only production version**, PromiseProof does not use Forge KVS or other app-managed persistent storage to retain selected Jira/Confluence content or saved commitments. The **Pin** control holds a temporary comparison snapshot in the current app session, not a permanent server-side record. Reloading or closing the session does not preserve a PromiseProof commitment ledger.

Atlassian hosts Forge and the underlying Jira/Confluence services. Atlassian may process and retain operational request data, authentication context or platform logs according to its own agreements, retention practices and privacy policies. Atlassian's Forge installation screen indicates that the app publisher may access **Forge application logs for troubleshooting** when vendor log access is enabled. These logs may contain technical errors or request metadata. Site administrators can inspect logs and can disable the publisher's log access through Atlassian administration. PromiseProof does not control Atlassian-managed retention; the publisher does not use Forge KVS to create a persistent commitment ledger in this release.

## Sharing and external services

The current app does not configure external egress endpoints and does not send selected Jira/Confluence content to a developer-operated external server. It does not sell user data or use data for targeted advertising. The app communicates with Atlassian services required to retrieve the sources that the signed-in user selected.

Do not enter confidential or personal information in public GitHub support issues. GitHub handles information that you submit on GitHub under GitHub's own policies.

## Your choices and requests

Use only Atlassian content for which you have permission. You can stop using the app and ask your site administrator to uninstall it. To request privacy information or report a concern, [open a support issue](https://github.com/ShenJun93/promiseproof-codegeist-docs/issues) without posting confidential data.

If a future release introduces permanent storage, new scopes or different data handling, this policy will be updated before such functionality is distributed.

## Updates

This policy describes the read-only PromiseProof Forge app distributed as of November 5, 2026. Changes to this document will be published in the repository history. PromiseProof is an independent project, not an official Atlassian product.
