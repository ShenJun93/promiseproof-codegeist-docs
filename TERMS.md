# PromiseProof — Terms of Service

**Effective date:** November 5, 2026  
**Project:** PromiseProof — Commitment Impact (independent Atlassian Forge app)  
**Contact:** [GitHub Issues](https://github.com/ShenJun93/promiseproof-codegeist-docs/issues)

## Purpose and scope

PromiseProof is a read-only decision-support tool. It compares a user-attested delivery commitment in selected Confluence text with selected Jira issue evidence. It may show date alignment, observed changes, explicit evidence gaps and hypothetical “what-if” outcomes. Results apply **only to the sources selected and successfully read**; they are not a complete dependency map.

PromiseProof does not validate that software was actually delivered, formally approve a release, enter a contract, or make a binding business decision.

## Who may use it

Use PromiseProof only on Atlassian sites where a site administrator has authorized its installation, and only with Jira and Confluence information you are entitled to read. Do not use it to circumvent permissions, scrape other users' data or make unsupported claims about project completion.

## Read-only behavior

The currently distributed production app requests the Atlassian scopes `read:jira-work` and `read:page:confluence`. It does not write to Jira or Confluence, and its “what-if” calculations do not modify actual deadlines. Session comparison snapshots are temporary. New features or scope changes require a later release.

## Interpretation and human responsibility

Data can be incomplete, outdated, inaccessible or scoped incorrectly. An `ON_TRACK` result means only that selected date evidence appears aligned; it is **not** proof of delivery, acceptance, quality, compliance or risk-free execution. An `UNKNOWN` result must not be treated as approval. Users are responsible for reviewing original Atlassian sources and making their own decisions.

## Availability and warranties

The app is offered for evaluation on an “as is” and “as available” basis, without a promise of uptime, accuracy, fitness for a particular purpose or continued maintenance. To the extent permitted by applicable law, the publisher is not liable for decisions made solely on its outputs. Nothing here removes rights that cannot legally be excluded.

## Third-party services and privacy

Your use of Jira, Confluence, Forge and GitHub is also subject to their applicable terms. For data-handling details, see the [Privacy Policy](./PRIVACY.md). PromiseProof is an independent project and is not endorsed by Atlassian.

## Changes and support

These terms may change as the app evolves. Changes will be visible in repository history. To report defects or request support, use [PromiseProof GitHub Issues](https://github.com/ShenJun93/promiseproof-codegeist-docs/issues); do not post private Jira or Confluence content in public issues.
