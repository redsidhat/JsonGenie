# Ansible Project Overview

This Ansible project is designed to automate the retrieval and processing of JSON data across two nodes, referred to as `nodeA` and `nodeB`. It includes roles for fetching JSON data, and separate processing for each node based on the length of alphanumeric characters in the data.

## Quick Setup

### Requirements

- Ansible installed on your control machine.
- Docker and Docker Compose for local testing.
- SSH keys configured for Docker containers.

### Structure

- `roles/`: Contains `json_retrieval`, `process_nodeA`, and `process_nodeB` roles.
- `hosts`: Inventory file to specify connection details for `nodeA` and `nodeB`.
- `main.yml`: Main playbook that incorporates roles and targets.

### Docker Testing Environment

Use Docker Compose to simulate `nodeA` and `nodeB` for testing:

1. **Start Containers**: `docker-compose up -d`
2. **Stop Containers**: `docker-compose down`

Docker Compose setup details are provided in the `docker-compose.yml` file, including SSH setup for container access.

### Running the Playbook

Execute the playbook with:

```bash
ansible-playbook main.yml --tags all,print_sum_nodeA,print_sum_nodeB,debug -i hosts

```

For targeted execution, use tags:

- `all`: Runs all tasks (default behavior).
- `print_sum_nodeA`: Specifically for printing the sum of lengths on nodeA.
- `print_sum_nodeB`: Specifically for printing the sum of lengths on nodeB.
- `debug`: Runs debug tasks

### Optional url overriding
```sh
-e "json_data_url=https://new.url.json"
```
### Inventory Configuration

Modify the `hosts` file to match your setup, ensuring correct addresses and SSH configurations for `nodeA` and `nodeB`, or to target the Docker containers:

```ini
[all:vars]
ansible_user=root
ansible_ssh_private_key_file=~/.ssh/id_rsa

[nodeA]
nodeA1 ansible_host=localhost ansible_port=2222

[nodeB]
nodeB1 ansible_host=localhost ansible_port=2223


```

## Notes

- Ensure Docker has access to your SSH public key at `~/.ssh/id_rsa.pub`.
- Adjust the Docker Compose file and `hosts` inventory as needed for your environment.
- Hmm.. May be use the official ubuntu container


## Todo
Create new user on the hosts with docker compose and use `become` to get root sudo