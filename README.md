# capz-prow-ai-dashboard

AI-powered dashboard for [Cluster API Provider Azure](https://github.com/kubernetes-sigs/cluster-api-provider-azure) E2E tests.

Deployed at **https://willie-yao.github.io/capz-prow-ai-dashboard/**.

## How this repo works

All the dashboard logic — Go fetcher, React frontend, AI prompts — lives in
[`willie-yao/prow-ai-dashboard`](https://github.com/willie-yao/prow-ai-dashboard).
This repo is a thin consumer that:

1. Selects a project config: [`configs/capz/project.yaml`](https://github.com/willie-yao/prow-ai-dashboard/blob/main/configs/capz/project.yaml) in the engine repo.
2. Calls the engine's reusable workflow on a 30-minute cron.
3. Stores the resulting site on its own `gh-pages` branch.

To tweak CAPZ-specific config (testgrid dashboard, cluster prefix, AI prompt, etc.)
edit `configs/capz/project.yaml` in the engine repo.

## Required secrets

Set these under **Settings → Secrets and variables → Actions**:

- `AI_TOKEN` — token for the chat completions endpoint (used for failure analysis).
- `SLACK_WEBHOOK_URL` — webhook for failure notifications (optional).

## Required settings

- **Settings → Pages → Source**: `GitHub Actions`.

## Forcing a fresh AI run

Run the `Clear AI Cache` workflow under the **Actions** tab to wipe the cache,
then re-run `Deploy Dashboard`.

