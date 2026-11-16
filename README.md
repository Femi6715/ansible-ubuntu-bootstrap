# Ansible: Ubuntu Server Bootstrap

An Ansible playbook that turns a fresh Ubuntu server into a basic web host.

## What the playbook does

1. Updates the apt package cache
2. Installs Docker and Nginx
3. Starts Docker and enables it at boot
4. Creates a `devops` user with a Bash shell and adds it to the `docker` group
5. Publishes a simple test page at `/var/www/html/index.html`
6. Starts Nginx and enables it at boot

Every task is idempotent, so running the playbook again changes nothing on a server that is already configured.

## Setup

Edit `inventory.ini` with your server's IP address and SSH user:

```ini
[web]
your_server ansible_host=1.2.3.4 ansible_user=ubuntu
```

## Usage

```bash
# Check the connection
ansible web -m ping

# Preview the changes
ansible-playbook playbook.yml --check

# Apply
ansible-playbook playbook.yml
```

Then open the server's IP in a browser to see the test page.

## Files

| File | Purpose |
|---|---|
| `playbook.yml` | The bootstrap tasks |
| `inventory.ini` | Target hosts |
| `ansible.cfg` | Points to the inventory and turns off retry files |
