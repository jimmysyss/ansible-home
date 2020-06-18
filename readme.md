ssh-copy-id jimmy@192.168.1.188

ansible-galaxy collection install -r requirements.yml 

ansible-galaxy role install -r requirements.yml 

ansible-playbook -i production site.yml --limit home -K

sudo rm -rf /var/lib/dpkg/lock-frontend /var/lib/dpkg/lock