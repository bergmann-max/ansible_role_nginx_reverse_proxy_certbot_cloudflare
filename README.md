# Ansible Role: nginx_reverse_proxy_certbot_cloudflare

![Ansible](https://img.shields.io/badge/ansible-ready-blue.svg)
![Platform](https://img.shields.io/badge/platform-Ubuntu-lightgrey)
![License](https://img.shields.io/badge/license-MIT-green)

## Description

This Ansible role installs and configures **Nginx** as a **reverse proxy** with **Let's Encrypt SSL certificates**, automatically issued using **Certbot** with **Cloudflare DNS challenge**.  
It ensures secure and automated SSL setup while managing Nginx virtual host configurations seamlessly.

### Features:
- Supports **Ubuntu systems**
- Configures **Nginx reverse proxy** for any backend port
- Automatically issues and renews SSL certificates via **Certbot**
- Uses **Cloudflare API token** for DNS challenge
- Provides **secure configuration** with sane defaults
- Includes **handlers** for smooth Nginx reloads/restarts
- Follows **Ansible role best practices** (clean structure, sane defaults, minimal dependencies)

---

## Supported Platforms

- Ubuntu (all versions)

---

## Role Variables

| Variable                     | Default Value                      | Description                                                                                   |
|------------------------------|------------------------------------|-----------------------------------------------------------------------------------------------|
| `domain`                     | `example.com`                      | The domain name for which Nginx and SSL certificates are configured                           |
| `backend_port`               | `3000`                             | Backend application port that Nginx proxies to                                                |
| `email`                      | `admin@example.com`                | Email address used for Let's Encrypt registration                                             |
| `cloudflare_api_token`       | `YOUR_CLOUDFLARE_API_TOKEN`        | API token used for Cloudflare DNS challenge (**must be encrypted with Ansible Vault!**)       |

> **Note:**  
> Sensitive variables like `cloudflare_api_token` should always be encrypted using **Ansible Vault** to follow security best practices.

---

## Usage Example

```yaml
- name: Setup Nginx Reverse Proxy with SSL via Cloudflare DNS
  hosts: all
  become: true
  roles:
    - role: ansible_role_nginx_reverse_proxy_certbot_cloudflare
      vars:
        domain: "mydomain.com"
        backend_port: 8080
        email: "admin@mydomain.com"
        cloudflare_api_token: "{{ vault_cloudflare_api_token }}"
```

---

## Tags

| Tag         | Purpose                                         |
|------------|-------------------------------------------------|
| nginx      | Install and configure Nginx                      |
| certbot    | Install and configure Certbot for SSL            |
| cloudflare | Configure Cloudflare DNS challenge               |
| ssl        | Manage Let's Encrypt SSL certificates            |
| reverseproxy | Setup Nginx reverse proxy                      |

---

## Sanity Checks

This role ensures:
- Nginx and Certbot are installed and configured correctly
- Cloudflare API token is securely stored and used
- Nginx reverse proxy configuration is templated and applied
- SSL certificates are issued and renewed properly
- Nginx is restarted or reloaded when configurations change
- Uses **handlers**, **tags**, and **default variables** for clean orchestration
- Conforms to Ansible directory and naming conventions

---

## Directory Structure

Follows Ansible Galaxy standard structure:
```
role/
├── defaults/
│   └── main.yml
├── handlers/
│   └── main.yml
├── meta/
│   └── main.yml
├── tasks/
│   └── main.yml
├── templates/
│   └── nginx.conf.j2
```
✔️ Clean, maintainable, and extensible!

---

## License

MIT

---

## Author Information

Role maintained by **Max Bergmann**.  
Contributions, improvements, and feedback are welcome! 🚀
