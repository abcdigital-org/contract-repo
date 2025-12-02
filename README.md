# Contracts Repository

This repository stores the canonical Pact contract files shared between consumers and providers.

## Structure

```
pacts/
  catalog-service/
  inventory-service/
```

Each provider owns a subdirectory that contains one JSON file per consumer. Consumer pipelines copy their freshly generated pact files into these folders and open a pull request against this repository. Provider pipelines check out the matching branch and verify the contracts during `repository_dispatch` events.

## Workflow

1. **Consumer** runs its pact tests, copies `pacts/*.json` into the appropriate provider directory, and opens a PR.
2. **Provider** responds to a `repository_dispatch` event, fetches the PR branch, and runs verification against the files in this repository.
3. Once all providers report success, merge the PR to make the contracts available on `main`.

> Tip: Protect the `main` branch and require PR approvals to ensure every contract change is validated by the relevant providers before merging.
