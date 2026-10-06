# yabe-linux

Ansible configuration for the Yabe range Linux team.

## Machines

| Hostname  | IP            | OS              | Role                    |
|-----------|---------------|-----------------|-------------------------|
| web01     | 10.30.10.10   | Ubuntu 22.04    | nginx, Apache, WordPress|
| mail01    | 10.30.10.11   | Fedora          | Postfix, Dovecot        |
| db01      | 10.30.10.12   | OpenSUSE Leap   | MariaDB, PostgreSQL, Redis |
| fs01      | 10.30.10.13   | Rocky Linux     | vsftpd, NFS, Samba, CA  |

## Setup

    # Install collections
    ansible-galaxy collection install -r requirements.yml

    # Copy secrets template and fill in real values
    cp vars/secrets.yml.example vars/secrets.yml

    # Dry run
    ansible-playbook site.yml --check --diff

    # Apply
    ansible-playbook site.yml

## Structure

    inventory/hosts.yml        <- target machines
    roles/                     <- one subdirectory per role
    vars/main.yml              <- non-secret variables
    vars/secrets.yml           <- secrets (never committed)
    vars/secrets.yml.example   <- secrets template (committed)
    site.yml                   <- entry point
    ansible.cfg                <- ansible settings

## Reference

- Planning document: yabe-range-planning-document.md
- Ansible docs: https://docs.ansible.com
