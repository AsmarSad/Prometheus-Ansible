# Prometheus-Ansible
## Project Structure
The project follows a modular structure, dividing tasks into roles for better organization and reusability:
```
.
├── ansible.cfg
├── main.yml
├── README.md
├── roles
│   ├── configure_prometheus
│   │   ├── defaults
│   │   │   └── main.yml
│   │   ├── tasks
│   │   │   └── main.yml
│   │   └── templates
│   │       └── prometheus.service.j2
│   └── provision_droplet
│       ├── defaults
│       │   └── main.yml
│       └── tasks
│           └── main.yml
└── secrets.yml
```

This playbook automates the creation of a DigitalOcean droplet, the installation, and configuration of Prometheus on it. 
# secrets.yml
Sensitive data such as `do_token` and `ssh_pub_key_path` are securely stored using Ansible Vault.
``` 
ansible-vault create secrets.yml
```
Inside secrets.yml:
```
do_token: "<digital_ocean_token>"
ssh_pub_key_path: "/path/to/key/file"
```
# First Task: Provisioning Droplets
Handles the creation of the DigitalOcean droplet:

✅ Uploads an SSH public key to DigitalOcean.

✅ Creates a droplet with specific configurations (name, size, region, etc.).

✅ Adds the new droplet's IP to the dynamic inventory.

# Second Task: Configuring Prometheus
Handles Prometheus installation and configuration:

✅ Installs required dependencies.

✅ Downloads and sets up Prometheus.

✅ Configures systemd service for Prometheus.

✅ Opens the required port (9090) in the firewall.

# Run Playbook
``` 
ansible-playbook main.yml --ask-vault-pass
```
## Result
✅ A DigitalOcean droplet with Prometheus installed and running.

✅ Prometheus accessible on port 9090 of the droplet's public IP.