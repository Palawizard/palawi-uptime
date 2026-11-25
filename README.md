# palawi-uptime

Checks the services hosted at home from outside the house. The monitoring that runs at home cannot report a power cut, a broken internet box or a dead server, so this check runs on GitHub Actions instead.

## What it checks

- Over HTTPS: `palawi.fr`, the PalaCards health endpoint, Authentik, the Drive, the MCP endpoint, Pala's Todo, AFFiNE and the dashboard. A 2xx, 3xx, 401 or 403 answer counts as up.
- Over TCP: the Minecraft server on `mc.palawi.fr:25567`.

Each check gets two tries, 60 seconds apart. If one still fails, the workflow posts the list of failing services to Discord and the run fails.

## When it runs

The workflow is scheduled every 30 minutes (`7,37 * * * *`). GitHub does not guarantee scheduled runs and skips many of them, so in practice there are a few hours between runs. It can also be started by hand: Actions tab, `uptime`, Run workflow.

## Setup

One repository secret, `DISCORD_WEBHOOK_URL`: the Discord webhook that receives the alerts.
