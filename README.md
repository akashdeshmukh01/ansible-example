# About project #

This is the example of ansible repository that shows how to organize managing your hosts with Ansible in one Git repository, how to use Ansible Galaxy and how to utilize [ansible-roles](https://github.com/andyceo/ansible-roles) repository with some common roles.


# System requirements #

This version of playbooks and roles was tested only on:

  - Ubuntu 14.04
  - Ansible 1.5.4 (shipped with Ubuntu 14.04 with enabled backports)

Previous versions of Ansible and Ubuntu are not supported. If you interested in its support, please, provide patches.

Tip: You can install ansible from this [PPA](https://launchpad.net/~rquillo/+archive/ansible): `sudo add-apt-repository ppa:rquillo/ansible` on systems older than Ubuntu 14.04


# Usage #

1. Install ansible on your manager machine:

        sudo aptitude install ansible
        
2. Clone this repository and change working directory to this repository (all following commands assumes that your working directory is this cloned repository directory):

        git clone git@github.com:andyceo/ansible-example.git
        cd ansible-example 
        
3. If you cloned repository `ansible-example` without submodules, then execute following commands in root folder of `ansible-example` repository to install `ansible-roles` repository:

        git submodule init
        git submodule update
        
4. Install andyceo roles from Ansible Galaxy:
   
        ansible-galaxy install andyceo.preconf andyceo.mailutils andyceo.mc andyceo.git andyceo.php andyceo.apache andyceo.composer andyceo.drush andyceo.mysql andyceo.phpmyadmin andyceo.nginx --force

5. Add your target (remote) host name you want to operate with (for example, `YOURTARGETHOSTNAME`) to inventory file: `ansible/hosts` or `ansible/hosts.py` (dynamic inventory)

6. Add file with your desirable config to `ansible/host_vars/YOURTARGETHOSTNAME`. Use `ansible/host_vars/ubuntu1310` as example

7. Run:

        ansible-playbook -K -k -v -i hosts -l <YOURTARGETHOSTNAME> example.yml --check --diff

    This will simulate playbook execute and show you posible difference that can be made by ansible. To execute playbook, just avoid `--check` and `--diff` modes:
   
        ansible-playbook -K -k -v -i hosts -l <YOURTARGETHOSTNAME> example.yml

    Also, you can execute playbook with dynamic inventory:

        ansible-playbook -K -k -v -i hosts.py -l <YOURTARGETHOSTNAME> example.yml
