# setup_alloy

This role installs Grafana Alloy on Ubuntu 24.04 and configures it to collect system metrics (node exporter), container metrics (cAdvisor), application metrics (configurable scrape targets), container logs (Docker), and journal logs, then forward everything to a Prometheus remote write endpoint and Loki push endpoint.

## Example usage and variables

```yaml
- hosts: all
  roles:
    - role: setup_alloy
      vars:
        # Optional, a custom Alloy config template (default: config.alloy.j2)
        alloy_config_alloy_template: "config.alloy.j2"

        # Required: Prometheus remote write endpoint
        alloy_prometheus_remote_write_url: "http://prometheus-host:9090/api/v1/write"
        # Required: Loki push endpoint
        alloy_loki_push_url: "http://loki-host:3100/loki/api/v1/push"
        # Required: shared basic auth credentials for both endpoints
        alloy_basicauth_username: "{{ lookup('env', 'ALLOY_BASICAUTH_USERNAME') }}"
        alloy_basicauth_password: "{{ lookup('env', 'ALLOY_BASICAUTH_PASSWORD') }}"

        # Required: project label added to all collected data
        alloy_project: "my-project"

        # Optional: additional Prometheus scrape targets (default: [])
        alloy_scrape_targets:
          - name: postgres
            address: "localhost:9187"
            metrics_path: "/metrics"
          - name: caddy
            address: "localhost:2019"
            metrics_path: "/metrics"
```
