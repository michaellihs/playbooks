# Ansible Playbooks for TYPO3 Server Team

This repository holds a collection of Ansible Playbooks for the management of the TYPO3 community servers

## Managing Git Repositories

    #!/bin/sh
    USER=myuser
    REPO=TYPO3CMS/Extensions/xxxx.git
    FORGE_REST_API=xxxx
    FORGE_PROJECT_ID=typo3cms-core

    ansible-playbook -v -i hosts -u ${USER} --extra-vars"delete_repo=${REPO}" -K playbooks/deletegitrepos.yml
    ansible-playbook -v -i hosts --extra-vars="forge_project_id=${FORGE_PROJECT_ID}  forge_api_key=${FORGE_API_KEY}  forge.yml

## Managing TYPO3 Users

### Setting up a Test Environment with Vagrant

Running the following commands, you get a Vagrant sandbox (running on IP 10.20.30.100) to test the Playbooks for user management:

    vagrant up
    vagrant ssh -c "sudo su -c \"useradd -m -s /bin/bash -p does_not_matter_set_it_later -G sudo ansible; echo -e \\\"ansible\nansible\\\" | (sudo passwd ansible)
\""
    # when asked for password, use 'ansible'
    ssh-copy-id ansible@10.20.30.100
    ansible-playbook -u <your username> -i hosts setup_vagrant.yaml


### Update email address for typo3.org user

Use the following ansible command to update the users on the servers configured in `hosts`:

    ansible-playbook -u <your username> -i hosts playbooks/t3org_email.yaml
