# yabe-firewall

Ansible configuration for the Yabe range firewall team.

## Devices

| Hostname       | IP           | Role                        |
|----------------|--------------|-----------------------------|
| vyos           | 10.30.1.1    | Border router, NAT          |
| debian-router  | 10.30.1.2    | Distribution router, ntopng |
| mikrotik       | 10.30.1.3    | Linux segment firewall      |
| pfsense        | 10.30.1.4    | Windows segment firewall    |

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
