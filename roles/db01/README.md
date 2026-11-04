# db01 Role

Provisioning DB01 database server for the Yave e-commerce platform.

## Services

**MariaDB** - Relational database for WordPress and web services
- Root password manages via secrets.yml
- Anonymous users removed
- Test database removed

**PostgreSQL** - Relational database for mail server
- Admin password managed via secrets.yml
- Password authentication enforced via pg_hba.conf
- Test database removed

**Redis** - In-memory cache and session store
- Password authentication required
- Bound to localhost only
- Data directory at /var/lib/redis

All tunable variables live in 'vars/main.yml'

## Usage

| Tag | Description |
|-----|-------------|
| 'db01' | Run all tasks across all services |
| 'infra' | Run all infrastructure tasks across all services |
| 'users' | Run all user management tasks across all services |
| 'mariadb' | Run all MariaDB tasks |
| 'postgresql' | Run all PostgreSQL tasks |
| 'redis' | Run all Redis tasks |

### Examples

### Run everything for db01
- ansible-playbook site.yml --tags db01

### Run only infrastructure across all services
- ansible-playbook site.yml --tags infra

### Run only MariaDB tasks
- ansible-playbook site.yml --tags mariadb

## Notes
- PyMySQL must be installed for Ansible to manage MariaDB
- psycopg2 must be installed for Ansible to manage PostgreSQL
- Redis uses template service redis@default on OpenSUSE
- User data hardening handled in security phase
