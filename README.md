# jershbytes.homelab

Ansible collection for homelab provisioning and post-provision configuration.

## Prerequisites

- Python 3.11+
- Ansible and ansible-lint (from [requirements-ansible.txt](requirements-ansible.txt))

## Local setup

```bash
git clone https://github.com/jershbytes/ansible-homelab.git
cd ansible-homelab

python -m venv .venv
source .venv/bin/activate
pip install -r requirements-ansible.txt

ansible-galaxy collection install -r requirements.yml
```

## Validate

```bash
ansible-lint
```

## Build the collection artifact

```bash
mkdir -p dist
ansible-galaxy collection build --output-path dist
```

This creates a tarball in [dist](dist) similar to:

```text
jershbytes-homelab-0.1.0.tar.gz
```

## Install locally from artifact

```bash
ansible-galaxy collection install dist/jershbytes-homelab-0.1.0.tar.gz --force
```

## Use from GitHub

Reference this repository in a requirements file:

```yaml
collections:
    - name: git+https://github.com/jershbytes/ansible-homelab.git
        type: git
        version: main
```

Then install:

```bash
ansible-galaxy collection install -r requirements.yml
```

## Publish a release on GitHub

Push a semantic version tag to trigger [release.yml](.github/workflows/release.yml):

```bash
git tag v0.1.0
git push origin v0.1.0
```

The workflow will:

- Run ansible-lint
- Build the collection tarball
- Create a GitHub Release and upload dist artifact(s)

## Prepare a release PR automatically

Run [release-pr.yml](.github/workflows/release-pr.yml) from the Actions tab with:

- version: 0.2.0
- release_summary: Short description of what changed

The workflow will:

- Bump version in [galaxy.yml](galaxy.yml)
- Add a new entry in [changelogs/changelog.yaml](changelogs/changelog.yaml)
- Run lint and build checks
- Open a PR named release/vX.Y.Z
