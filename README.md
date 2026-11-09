# linux_baseline

Base setup for every Linux machine in the homelab:

- Packages kept up to date, unused ones removed, and security updates installed unattended.
  It never reboots on its own.
- `nano`, `wget` and `iproute2` installed.
- Timezone `Europe/London` and locale `en_GB.UTF-8`.
- Time kept by chrony from the UK NTP pool.
- Passwordless sudo for the user Ansible logs in as.

Tested on Debian trixie (Raspberry Pi OS).

## Variables

| Variable | Default |
| --- | --- |
| `linux_baseline_packages` | `[nano, wget, iproute2]` |
| `linux_baseline_timezone` | `Europe/London` |
| `linux_baseline_locale` | `en_GB.UTF-8` |
| `linux_baseline_ntp_pool` | `uk.pool.ntp.org` |
| `linux_baseline_sudo_user` | `ansible_user` |

## Requirements

The `community.general` collection, pinned in `requirements.yml`.

## Usage

```yaml
- hosts: linux
  become: true
  roles:
    - linux_baseline
```

## Development

Tests run with Molecule in a Debian trixie container running systemd, and check the machine's real state.

```sh
pip install -r requirements-test.txt
molecule test
```

Commits follow Conventional Commits.
Releases are versioned and tagged automatically from `main`.
