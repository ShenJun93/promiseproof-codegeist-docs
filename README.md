# PromiseProof — Public Information

PromiseProof is an independent, **read-only Atlassian Forge app** for comparing an explicitly attested Confluence delivery commitment with live, selected Jira evidence. It helps teams see date risk, source changes, evidence gaps and hypothetical remediation choices without automatically modifying Jira or Confluence.

**For Codegeist reviewers:** use the **official installation URL supplied in the Devpost submission**. The installation requires **both Jira Cloud and Confluence Cloud on the same site**. The publisher's own demonstration source IDs do not work on other sites.

- [Judge installation and reproducible test guide](./JUDGE-QUICKSTART.md)
- [Privacy policy](./PRIVACY.md)
- [Terms of service](./TERMS.md)
- [Support and issue reports](https://github.com/ShenJun93/promiseproof-codegeist-docs/issues)

The current Forge production release requests `read:jira-work` and `read:page:confluence` and does **not** include persistent commitment storage/KVS, external egress or Atlassian write scopes.

This repository contains **public documentation only**. It is not the application source repository and contains no user data, credentials or private Atlassian fixtures.

PromiseProof is not affiliated with or endorsed by Atlassian.
