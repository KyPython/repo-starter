# repo-starter

Template for every new Ky repo. Governed from the first commit: it calls the
shared `ai-governance / verdict` gate, carries the `AI-GOVERNANCE:v1` agent
rules, and assigns every path to Ky for review.

## Use it

```bash
gh repo create <name> --template KyPython/repo-starter --public --clone
cd <name>
# work on branches, open PRs, Ky merges
```

After creating from this template, protect the default branch once the verdict
is green:

```bash
GITHUB_TOKEN=<pat> /Users/ky/ai-governance/scripts/optin.sh --protect KyPython/<name>
```

If a repo is created without the template, the daily governance sweep in
`KyPython/ai-governance` opens an opt-in PR within 24 hours.

## What the gate runs here

`quality` installs and runs `test` (add `lint`, `type-check`, `build` scripts
as the project grows; the gate runs whichever exist). `policy` checks
`AGENTS.md`, `CODEOWNERS`, pinned actions, PR title, and issue references.
`secret-scan` runs gitleaks. `verdict` aggregates fail-closed.

## Keeping the pin current

The caller pins an `ai-governance` commit SHA. After Ky merges gate changes,
bump the SHA in `.github/workflows/ai-governance.yml` in a PR Ky approves.
