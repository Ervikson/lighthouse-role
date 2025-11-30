# Ansible Role: lighthouse-role

Ansible role for installing and configuring Lighthouse - a web performance analysis tool from VKCOM.

## Description

This role installs Nginx web server, downloads Lighthouse static files from GitHub, and configures Nginx to serve them.

## Requirements

- Ansible >= 2.9
- Debian/Ubuntu based system
- Root or sudo access
- Internet connection for downloading Lighthouse files

## Role Variables

### Default Variables

| Variable | Default | Description |
|----------|---------|-------------|
| `lighthouse_download_url` | `"https://github.com/VKCOM/lighthouse/archive/refs/heads/master.zip"` | URL to download Lighthouse archive |
| `lighthouse_archive_path` | `/tmp/lighthouse.zip` | Local path where archive will be downloaded |
| `lighthouse_extracted_path` | `/tmp/lighthouse-master` | Path to extracted Lighthouse directory |
| `lighthouse_web_root` | `/var/www/lighthouse` | Web server root directory |
| `lighthouse_web_server` | `nginx` | Web server package name |
| `lighthouse_nginx_config_path` | `/etc/nginx/sites-available/lighthouse` | Path to Nginx configuration file |
| `lighthouse_nginx_site_enabled_path` | `/etc/nginx/sites-enabled/lighthouse` | Path to enabled Nginx site |
| `lighthouse_nginx_default_site_path` | `/etc/nginx/sites-enabled/default` | Path to default Nginx site |
| `lighthouse_download_timeout` | `300` | Download timeout in seconds |
| `lighthouse_apt_cache_valid_time` | `3600` | APT cache valid time in seconds |

### Example Playbook

```yaml
---
- hosts: lighthouse
  become: true
  roles:
    - lighthouse-role
```

### Customizing Variables

You can override default variables:

```yaml
---
- hosts: lighthouse
  become: true
  vars:
    lighthouse_web_root: /var/www/html/lighthouse
    lighthouse_web_server: nginx
  roles:
    - lighthouse-role
```

## Dependencies

None

## What This Role Does

1. Updates APT cache
2. Installs Nginx and unzip packages
3. Creates web root directory
4. Downloads Lighthouse static files from GitHub
5. Extracts the archive
6. Copies files to web root directory
7. Configures Nginx to serve Lighthouse
8. Enables Lighthouse site
9. Removes default Nginx site
10. Starts and enables Nginx service

## Example Playbook

```yaml
---
- name: Install Lighthouse
  hosts: lighthouse
  become: true
  roles:
    - lighthouse-role
```

After installation, Lighthouse will be available at `http://<host-ip>/`

## License

MIT

## Author Information

This role was created as part of the Ansible course project.
