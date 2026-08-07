
# Lab M5.07 - Configuration Management with Ansible

## What This Project Does

Ansible playbooks that configure a server with nginx, git, curl, application
directories, and a custom web server configuration. A GitHub Actions workflow
validates the playbooks on every push.

## Project Structure

\`\`\`
.
├── .gitignore               # Keeps .venv out of the repo
├── ansible.cfg              # Ansible defaults
├── inventory.ini            # Target hosts
├── group_vars/
│   └── all.yml              # Shared variables
├── templates/
│   └── app.conf.j2          # Application config template
├── roles/
│   └── webserver/           # Reusable webserver role
│       ├── tasks/main.yml
│       ├── templates/index.html.j2
│       ├── defaults/main.yml
│       └── handlers/main.yml
├── site.yml                 # Base configuration playbook
├── webserver.yml            # Web server playbook
├── role-webserver.yml       # Playbook that applies the role
└── .github/workflows/
    └── ansible-ci.yml       # CI pipeline
\`\`\`

## How to Run

\`\`\`bash

# Install Ansible

pip install ansible ansible-lint

# Dry-run base config

ansible-playbook site.yml --check --diff

# Dry-run web server config

ansible-playbook webserver.yml --check --diff

# Apply for real (requires sudo)

ansible-playbook site.yml
ansible-playbook webserver.yml
\`\`\`

## Key Decisions

- **Local connection** used for safe classroom testing
- **Jinja2 templates** for environment-specific configs
- **Role structure** keeps the webserver setup portable
