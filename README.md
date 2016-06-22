[![Build Status](http://img.shields.io/travis/cchurch/ansible-role-win-ec2.svg)](https://travis-ci.org/cchurch/ansible-role-win-ec2)
[![Galaxy](http://img.shields.io/badge/galaxy-cchurch.win--ec2-blue.svg)](https://galaxy.ansible.com/cchurch/win-ec2/)

Win-EC2
=======

Create and destroy Windows instances on EC2. Generate a static inventory file
usable for running additional playbooks against Windows hosts.

Role Variables
--------------

The following variables may be defined to customize this role:

- `win_ec2_region`: Region in which instances are created, default is `us-east-1`.
- `win_ec2_instance_type`: Instance type for creating instances, default is `m3.medium`.
- `win_ec2_security_group`: Name of security group to create/use for Windows instances, default is `win-ec2`.
- `win_ec2_security_group_description`: Description for security group, default is `Security group for Ansible WinRM`.
- `win_ec2_key_name`: Name of keypair created/used for Windows instances, default is `win-ec2`.
- `win_ec2_public_key_path`: Path to public key for creating keypair, default is `~/.ssh/id_rsa.pub`.
- `win_ec2_private_key_path`: Path to matching private key to use for decrypting Windows passwords, default is `~/.ssh/id_rsa`.
- `win_ec2_name_prefix`: Prefix for `Name` tag associated with each instance, default is `win-ec2`.
- `win_ec2_images`: List of AMIs to use for creating instances.  Each list item should be a hash
  containing `ami_id` and `name` keys.  Default is `{{win_ec2_default_images[win_ec2_region]}}`.
- `win_ec2_action`: Action to perform, should be one of `create`, `recreate` or `destroy`; default is `create`.
- `win_ec2_inventory_dest`: Path to write static inventory file, default is `{{playbook_dir}}/inventory.win-ec2`.

Valid AWS credentials must be specified either by setting `aws_access_key` and
`aws_secret_key` variables or by defining `AWS_ACCESS_KEY` and `AWS_SECRET_KEY`
environment variables.

Example Playbook
----------------

The following example playbook creates, then destroys Windows instances in EC2:

    - hosts: localhost
      vars:
        win_ec2_name_prefix: example
      roles:
        - role: cchurch.win-ec2
        - role: cchurch.win-ec2
          win_ec2_action: destroy

License
-------

BSD

Author Information
------------------

Chris Church <chris@ninemoreminutes.com>
