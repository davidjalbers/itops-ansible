# deploy-traefik

This role deploys the Traefik reverse proxy as a Docker Compose stack.

## Example usage

```yaml
---
- hosts: all
  roles:
    - deploy_traefik
  vars:
    traefik_domains:
      - "demo-server.example.com"
    traefik_letsencrypt_email: "letsencrypt@example.com"
    b_traefik_configure_metrics: true
    b_traefik_configure_dashboard: true
    traefik_dashboard_host: "traefik.{{ traefik_domains[0] }}"
    traefik_cloudflare_api_token: "{{ lookup('env', 'TRAEFIK_CLOUDFLARE_API_TOKEN') }}"
```
