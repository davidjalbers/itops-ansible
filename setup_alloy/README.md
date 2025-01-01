# setup_alloy

This role installs Grafana Alloy on Ubuntu 24.04.

## Example usage and variables

```yaml
- hosts: all
  roles:
    - role: setup_alloy
      vars:
        # Optional, a default template will be used if not provided
        alloy_config_alloy_template: "<custom-alloy.j2.config>"

        # Optional, enables metric scraping from Traefik. Defaults to false
        b_alloy_configure_traefik_metrics: true
        # Optional, defaults to localhost:9090 and is only used if b_alloy_configure_traefik_metrics is true
        alloy_traefik_metrics_endpoint: "<desired endpoint>"

        # Optional, enables log scraping from Docker. Defaults to false
        # If set to true, requires the docker group to be present on the target systems
        b_alloy_configure_docker_logs: false

        # Optional, adds xproject labels to collected data. Defaults to false
        # If set to true, requires the xproject_name, xproject_namespace, and xproject_environment variables to be defined
        b_alloy_configure_xproject_labels: false

        # These six are all required
        alloy_prometheus_endpoint: <ENTER_PROMETHEUS_ENDPOINT_HERE>
        alloy_prometheus_basicauth_username: "{{ lookup('env', 'ALLOY_PROMETHEUS_BASICAUTH_USERNAME') }}"
        alloy_prometheus_basicauth_password: "{{ lookup('env', 'ALLOY_PROMETHEUS_BASICAUTH_PASSWORD') }}"
        alloy_loki_endpoint: <ENTER_LOKI_ENDPOINT_HERE>
        alloy_loki_basicauth_username: "{{ lookup('env', 'ALLOY_LOKI_BASICAUTH_USERNAME') }}"
        alloy_loki_basicauth_password: "{{ lookup('env', 'ALLOY_LOKI_BASICAUTH_PASSWORD') }}"

```
