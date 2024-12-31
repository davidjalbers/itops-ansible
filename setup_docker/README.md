# setup_docker

This role installs Docker on Ubuntu 24.04.

## Example usage and variables

```yaml
- hosts: all
  roles:
    - role: setup_docker
      vars:
        # Optional, a default daemon.json template will be used if not provided
        docker_daemon_json_template: "<custom-daemon.json.j2>" 
```
