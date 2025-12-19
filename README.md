# Redmine + GitLab Cluster  
**VirtualBox · Vagrant · Ansible · systemd services**

This project provisions a **local multi-VM cluster** consisting of:

- **Redmine** (installed from source, running as a systemd service — no Docker)
- **PostgreSQL** (database backend for Redmine)
- **GitLab EE (Omnibus)** running **behind an external Nginx reverse proxy**
- **Nginx** acting as the single entry point with TLS termination

The entire environment is defined as code using **Vagrant** (VM lifecycle) and **Ansible** (configuration & services).

---

## Architecture Overview

```
Host → Nginx → Redmine
            → GitLab
          ↘ PostgreSQL
```

---

## VM Layout & IP Addresses

| Service     | VM Name   | IP              |
|------------|-----------|-----------------|
| Nginx      | nginx     | 192.168.56.10   |
| Redmine    | redmine   | 192.168.56.11   |
| PostgreSQL | postgres  | 192.168.56.12   |
| GitLab     | gitlab    | 192.168.56.13   |

---

## Requirements

- VirtualBox
- Vagrant
- Ansible

Install required Ansible collections:

```
ansible-galaxy collection install -r ansible/requirements.yml
```

---

## Quick Start

```
vagrant up
```

Add to hosts file:

```
192.168.56.10 redmine.local
192.168.56.10 gitlab.local
```

Open:

- https://redmine.local
- https://gitlab.local

---

## Notes

- TLS certificates are self-signed (lab setup)
- GitLab requires at least 8 GB RAM
- Redmine runs as a native systemd service

---

## License

Internal / educational use.