# deploy-traefik

This role deploys the Traefik reverse proxy as a Docker Compose stack.

## Example usage and variables

```yaml
---
- hosts: all
  roles:
    - deploy_traefik
  vars:
    # Optional. A default version is set in defaults/main.yml
    traefik_version: "<desired version>"
    # Optional. A default template will be used if not set
    traefik_compose_yaml_template: "<custom-compose.j2.yaml>"
    # Optional. A default template will be used if not set
    traefik_traefik_yml_template: "<custom-traefik.j2.yml>"

    # WHEN USING THE DEFAULT TEMPLATES, THE BELOW VARIABLES ARE USED / REQUIRED

    # Required. Docker network to create for Traefik and service containers
    traefik_network_name: "traefik_public_network"

    # Required. Configuration for automatic Let's Encrypt certificate generation with DNS-01 challenge
    traefik_domains:
      # This will obtain a cert for demo-server.example.com and *.demo-server.example.com 
      - domain: "demo-server.example.com"
        b_wildcard: true
      # This will obtain a cert for myapp-production.example.com
      - domain: "myapp-production.example.com"
      # If you don't need further config, this shorthand will also obtain a cert for accounts.example.com
      - "accounts.example.com"
    traefik_letsencrypt_email: "letsencrypt@example.com"
    traefik_cloudflare_api_token: "{{ lookup('env', 'TRAEFIK_CLOUDFLARE_API_TOKEN') }}"

    # Prometheus metrics configuration
    b_traefik_configure_metrics: true
    # Optional. Defaults to 9090 and is only used if b_traefik_configure_metrics is true
    traefik_metrics_port: "<desired port>"

    # If true, only enables the dashboard service in the static configuration.
    # You still need to configure a router for it, e.g. with a file in the dynamic configuration directory (/opt/stacks/traefik/conf.d).
    b_traefik_configure_dashboard: true

    # Optional. A list of CIDRs to trust as proxies, from which X-Forwarded-For and X-Real-IP headers are accepted.
    traefik_trusted_cidrs:
      - "172.45.0.0/16"
      - "2a00:1388:5000:120::/64"

    # Optional. A list of CIDRs to use as whitelist for the 80 and 443 entrypoints. If set, all other IPs will be denied.
    traefik_whitelist_cidrs:
      - "172.45.0.0/16"
      - "2a00:1388:5000:120::/64"
```
