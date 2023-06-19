# ansible
ansible training
cmds:
	- ansible all -m apt -a "upgrade=dist" --become --ask-become-pass
	- ansible all -m apt -a "name=tmux state=latest"
	- ansible-playbook install_apache.yml --ask-become-pass
	- ansible all -m gather_facts | grep ansible_dist
	- sudo firewall-cmd --add-port=80/tcp # allow communication with the port 80 (i.e; httpd)
	- sudo systemctl start httpd # to start the httpd service
