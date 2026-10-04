# Initial Deployment Requirements
## How to include alertmanager in a stack

```yaml
services:
  alertmanager:
    extends:
      file: ../../containers/alertmanager/compose.yaml
      service: .alertmanager
```

## Alert routing
`config/alertmanager.yml` sends every alert as mail to `infra@mailrise.xyz` on the mailrise container of the core-infra stack, which posts it to the ntfy `alerts-infra` topic. The ntfy token is in `mailrise.conf`, so Alertmanager's config holds no secret.

Alertmanager reaches mailrise by its container name, `core-mailrise`, over the shared proxy network. Both stacks have to run on the same host. If they do not, change `smtp_smarthost` to the other host's address and mailrise's published port.
