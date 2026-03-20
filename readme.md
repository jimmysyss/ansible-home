This is my test for Ansible, this is the commands I used

After installing a brandnew system, use this command to enable SSH cert based auth (no password needed)
```
ssh-copy-id jimmy@192.168.1.188
```

Install Ansible Collections and Roles locally, -K means prompt for Sudoer password
```
ansible-galaxy collection install -r requirements.yml 
ansible-galaxy role install -r requirements.yml 
ansible-playbook -i inventory/production site.yml --limit home -K
```

Because my script uses APT, Ubuntu may lock down the DPKG update, you may need to remove the lock file
```
sudo rm -rf /var/lib/dpkg/lock-frontend /var/lib/dpkg/lock
```

Ubuntu 18.04 comes with Ansible 2.5, which is quite old, you need to install Ansible 2.8 or 2.9 with the following commands
```
sudo apt update
sudo apt install software-properties-common
sudo apt-add-repository --yes --update ppa:ansible/ansible
sudo apt install ansible
```


ansible-playbook -i inventory/production site.yml --limit desktop1 -K --private-key ~/.ssh/oracle_cloud

eval "$(ssh-agent -s)"
ssh-add ~/.ssh/oracle_cloud

pip3 install PyMySQL

Validate syntax before any live run:
```
ansible-playbook -i inventory/production site.yml --syntax-check
```

Issue #5 validation target (server8):
```
ansible-playbook -i inventory/production site.yml --limit server8.jimmysyss.com --check --diff -K
ansible-playbook -i inventory/production site.yml --limit server8.jimmysyss.com -K
```