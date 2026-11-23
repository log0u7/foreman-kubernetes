# Foreman on Kubernetes

## Build and test

- Lint: `make lint`
- Integration: `make setup-test-env`, `make setup-kind`, `make test`
- Diagnostics: `make diagnostics`; cleanup: `make teardown-kind`
- Integration uses native Linux AMD64 and defaults to Podman; see
  `docs/quick-start.md` for dependencies and privileges.
- Test deps live in `tests/requirements.txt` (pytest, pytest-helm-charts:
  the `kube_cluster` fixture comes from that package, not from the repo).
  Always install with `pip install -r tests/requirements.txt`; plain
  `pip install pytest` fails the suite with a missing-fixture error.
- Candidate image validation overrides the chart image through env vars
  only: `HELM_IMAGE_REPOSITORY` / `HELM_IMAGE_TAG` (see
  `.github/workflows/candidate.yaml`). Unset means chart defaults.
- After pushing a NEW image package to GHCR, the package is private by
  default: flip it public in the UI (API does not expose visibility)
  or anonymous pulls (kind, CI) fail with 403. Verify with
  `docker manifest inspect ghcr.io/<owner>/<name>:<tag>`.

## Project pointers

- `README.md`: project scope, boundaries, and status. The project is experimental
  and unsupported.
- `CONTRIBUTING.md` and `.github/PULL_REQUEST_TEMPLATE.md`: contribution and
  pull request guidance.
- `docs/roadmap.md`: intended high-level sequence, not a live task tracker; use
  the linked issues and project board for current status.
