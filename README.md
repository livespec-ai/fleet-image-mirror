# fleet-image-mirror

Copies the livespec fleet's pinned container images from `ghcr.io/thewoolleyman` to
`ghcr.io/livespec-ai` **by digest**, ahead of the move of the fleet repositories into the
livespec-ai organization. Plan `stale-base-merge-options` (livespec-dev-tooling epic
livespec-dev-tooling-xowhol), work item livespec-dev-tooling-yqpwy3.

Run `mirror` (workflow_dispatch) with one `name tag sha256:digest` triple per line. It uses only
`GITHUB_TOKEN`, with `packages: write`. A GitHub App installation token cannot create an
organization package: GHCR answers 403 "installation not allowed to Create organization package".

Re-run it at the cutover halt with the then-current pinned tags.

Pull requests land on main through the livespec-ai merge queue (ruleset master-incident-recovery-bypass); ci-green is the required check.

The merge-group-guard job skips a merge group whose tree equals the pull request head tree.
