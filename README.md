## AWS Infra deployment example playbooks

- Playbooks available:
  - [EC2 launch example](./ec2_launch.yml) - [guide](https://github.com/silazare/aws-ansible#aws-deployment-for-ubuntu-1604nginxansible)
  - [EC2 facts collection example](./ec2_facts.yml)
  - [EC2 custom AMI cleanup example](./ami_cleanup.yml)
  - [ECS cluster playbook example](./ecs_cluster.yml)

### AWS deployment for Ubuntu 16.04+Nginx+Ansible.

- Clone this repository to your folder:
```sh
$ git clone https://github.com/silazare/aws-ansible.git
$ cd aws-ansible
```

- Create vault file with your aws keys:
```sh
$ ansible-vault create secret.yml
secret_key: XXXXXX
access_key: XXXXXX
$ ansible-vault view secret.yml
```

- Create vault_pass file with plain password for playbook simple run and test it:
```sh
$ ansible-vault view secret.yml --vault-password-file=vault_pass
```

- Configure group_vars for your region/ami/vpc/lifetime and move group_vars/all_example into all.yml
- Static HTML is created from simple Google Doc as a demo, you may change this approach as you want.

- Execute playbook and check web page at ELB hostname:
```sh
ansible-playbook ec2_launch.yml --vault-password-file vault_pass
```

- Check instances in AWS console after creation/destroy.

### AWS deployment for ECS cluster.

- Clone this repository to your folder and repeat the same configuration steps as described [here](https://github.com/silazare/aws-ansible#aws-deployment-for-ubuntu-1604nginxansible)

- Playbook execution to create ECS cluster with example of services:
```sh
ansible-playbook ecs_cluster.yml --extra-vars="ecs_state=present" --vault-password-file vault_pass
```

- Playbook execution to destroy ECS cluster with all related services:
```sh
ansible-playbook ecs_cluster.yml --extra-vars="ecs_state=absent" --vault-password-file vault_pass
```

TBD:
1) Custom healthcheck for post service - https://github.com/ansible/ansible/issues/50024
2) Link all microservices within ALB target groups
3) More parametrize for ALB rules
4) No idempotency for target groups creation several times  - https://github.com/ansible/ansible/pull/39715