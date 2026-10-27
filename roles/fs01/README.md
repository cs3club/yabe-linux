# fs01 Role

Provisioning FS01 file server for the Yabe e-commerce platform.

## Services

**Samba** - Windows-accessible file shares!
- 'admin' share - rw for IT admins
- 'staff' share - ro for general staff

**NFS** - Linux-to-Linux file sharing!
- Exports vendor directory for web server read access
- 'yabe_web' service account with fixed UID for NFS permission consistency, preventing issues

**vsftpd** - FTP/FTPS server for vendor file uploads
- Vendors chrooted to their own directories
- Passive mode configured on ports 40000-40100
- Current vendors:
	- JoystickJunction - Retro Arcade Reseller
	- HamChan Imports - Hamtaro Merch Shop

All tunable variables live in 'vars/main.yml'.

# Usage

| Tag | Description |
|-----|-------------|
| 'infra ' | Run all infrastructure tasks across all services |
| 'users' | Run all user management tasks across all services |
| 'samba' | Run all Samba tasks |
| 'nfs' | Run all NFS tasks |
| 'vsftpd' | Run all FTP tasks |

### Examples

#### Run everything for one service
- ansible-playbook site.yml --tags samba

#### Run only user management across all services
- ansible-playbook site.yml --tags users

#### Run only FTP infrastructure, no user management
- ansible-playbook site.yml --tags vsftpd --skip-tags users

## Notes
- DNS record 'ca.yabe.corp -> 10.30.10.13' must be created on DC01 before TLS (used in FTPS) can be configured
- NFS UID for 'yabe_web' must match on the web server (UID 1500)
- FTPS and security hardening handled in security phase
