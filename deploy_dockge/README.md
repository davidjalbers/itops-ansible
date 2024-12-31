# deploy_dockge

This role is used to deploy **dockge** with Docker Compose.

Note that this role only creates the necessary files and directories, and does not actually run the application. 
To start dockge, you need to run `docker compose up -d` in `/opt/dockge` (where `compose.yaml` is located).
This is because the first time you run dockge, the web interface will offer the possibility create the superuser and this is something that shouldn't be automated.

## Example usage and variables

```yaml
- hosts: all
  roles:
    - role: deploy_dockge
      vars:
        # Optional, a default version will be used if not provided
        dockge_version: "1.0.0"
        # Optional, defaults to false. If set to true, requires dockge_traefik_host and dockge_traefik_network_name
        b_dockge_add_traefik_configuration: true 
        dockge_traefik_host: "dockge.example.com"
        dockge_traefik_network_name: "traefik_public_network"
```
