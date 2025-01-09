# setup_tailscale

This role installs tailscale.

## Example usage and variables

```yaml
- name: Install Tailscale
  hosts: all
  roles:
    - role: setup_tailscale
      vars:
        b_tailscale_enable_userspace_networking: false
```
