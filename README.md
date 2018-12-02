## AWS Infra deployment example playbooks

- Playbooks available:
  - EC2+ELB+2SG+NGINX+Simple HTML page auto creation and destroy after defined lifetime expired.
  - EC2 facts collection example which could be used for playing different tasks on it.
  - EC2 custom AMI cleanup example.

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
