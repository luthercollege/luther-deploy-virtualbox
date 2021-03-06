# Virtual box for Luther College's Ansible playbooks

## Introduction
The luther-deploy-virtualbox repository contains an Ubuntu virtual box with the GitHub repository https://github.com/luthercollege/ansible. It has a more current version of Ansible installed than is present on Mac OSX so newer Ansible features can be used. It also ensures that developers are using the same Linux platform for deployment.

## Getting started
- make sure you have access to the private repository https://github.com/luthercollege/ansible
- confirm that you have an existing public and private key pair in your home directory (~/.ssh/id_rsa and ~/.ssh/id_rsa.pub)
- at a terminal prompt type `ssh -T git@github.com` to test your connection to your github account
- if the connection fails then see https://help.github.com/articles/adding-a-new-ssh-key-to-your-github-account/

- assuming your on a Mac OS machine, confirm that the XCode command line tools are installed: xcode-select --install
- download and install the virtual box app (https://www.virtualbox.org/wiki/Downloads)
- download and install Vagrant (https://www.vagrantup.com/downloads.html)
- pip is needed: sudo easy_install pip
- you'll need Ansible locally to configure the VM: sudo pip install ansible --quiet
- clone or download the contents of this repository by opening a terminal window and typing `git clone git@github.com:luthercollege/luther-deploy-virtualbox.git`
- then in the same terminal application: `cd luther-deploy-virtualbox`
- type `vagrant up` to start and provision the virtual box (may take a few minutes)

## Using for deployment
- once the virtual box is up and running type `vagrant ssh` to access at IP address 192.168.56.110
- a user with the same name as your local username was also created on the virtual box so `sudo su <username>` to login as yourself (e.g. `sudo su jonebr01`)
- `cd ~/ansible` to  to view the contents of the Luther College ansible playbooks used for deployment
- test connection to reasondev.luther.edu by typing `ansible reasondev -m ping -vvv`
- deploy to reasondev.luther.edu by entering `ansible-playbook site.yml --limit reasondev -K --tags=deploy`
- git is installed so you can commit and push any changes you made to the Luther ansible repository, or fetch, merge, and rebase updates made by other developers directly from the virtual box. (Note that before you commit to Github initially you will need to add the name and email associated with your Github account to ~/.gitconfig: `git config --global user.email "you@example.com"` and `git config --global user.name "Your Name"`)
