# Ansible Playbook to sync iplist with Fortigate Addressgroup
This ansible playbook downloads an ip list separated by line break and creates address objects on the fortigate firewall for every item in the list. A new firewall address group will be created and every item in the ip list will be added as member. In addition, orphan address objects (not in the iplist anymore), will be DELETED from the fortigate firewall. A prefix to the name of the address objects will be added and used to detect stale entries.

## Installation
1. Create a new python environment if needed
```bash
python3 -m venv ansible_venv
```
2. Install Ansible
```bash
# if a python virtual environment has been created...
. ansible_venv/bin/activate
pip3 install ansible-base
```
3. Install fortigate collection
```
ansible-galaxy install -r collections/requirements.yml
```
4. Prepare ansible inventory. Create a new inventory file named `hosts`.
```
fw.example.local
```

## Execution
1. Adjust the variables in the playbook (Prefix for the address objects, URL of the iplist).
2. Get a Rest API token from the fortigate.
3. Inject API token as environment variable and execute the playbook.
```
export FORTI_TOKEN=token
ansible-playbook -i hosts forti-sync-iplist.yml
```
