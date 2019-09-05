# drone-aws-ansible
Deploys Droneio on an aws instance

## Modify vars files

### Files on drone-aws/vars/mainl.yml
```yaml
security_group_name: {{ Your drone security group name}}
security_group_description: {{ Your security group description }}
drone_region: {{ Your region }}
drone_instance: {{ Your instance type }}
drone_key: {{ Your drone key }}
drone_image: {{ Your image }}
drone_count: 1
drone_subnet: {{ Your subnet }}
drone_group: {{ Your drone group }}
drone_tag: {{ Your drone tag }}
```

### Files on setup-drone/vars/mainl.yml
```yaml
# drone server variables
drone_server_version: 1
drone_server_name: {{ Your drone isntance name }}
my_client_id: {{ Your client id }}
my_client_secret: {{ Your client secret }}
rpc_secret: {{ Your rpc secret }}

# drone agent variables
drone_agent_version: 1
drone_agent_name: {{ Your drone agent name }}
```

For further drone configuration consult the documention on [Drone CI](https://drone.io/).

### Different instance's user name

In case you have a different intance user, you can modify it on the install-docker roll, you'll find the file at install-docker/vars/main.yml:

```yaml
#vars for install-docker
user: ec2-user
group: docker
```

You'll also need to modify the main playbook at the second task:
```yaml
- name: Deploy drone
  hosts: drone-group
  remote_user: ec2-user
  become: yes
  gather_facts: no
  roles:
    - install-docker
    - setup-drone
```
