# Semaphore Ansible Test

Minimal Ansible project for validating Semaphore UI execution.

## What it checks

- Hostname
- Uptime
- OS and architecture
- Disk usage
- Memory
- `/etc/fstab` on Linux
- Running systemd services on Linux
- Failed systemd services on Linux

The playbook automatically uses `vm_stat` on macOS and `free -h` on Linux.

## Repository layout

```text
semaphore-ansible-test/
├── ansible.cfg
├── inventory/
│   └── hosts.yml
└── playbooks/
    └── test.yml
```

## Local test

```bash
ansible --version
ansible-inventory -i inventory/hosts.yml --graph
ansible-playbook -i inventory/hosts.yml playbooks/test.yml
```

## Semaphore configuration

Create a Semaphore project and add this Git repository.

Use:

- Repository branch: `main`
- Inventory file: `inventory/hosts.yml`
- Playbook: `playbooks/test.yml`

No SSH credentials are required for this localhost test.

## Important

If Semaphore runs directly on macOS, `localhost` is the Mac.

If Semaphore runs in Docker, `localhost` is the Semaphore container, not the Mac host.

This project performs checks only. It does not patch or reboot anything.
