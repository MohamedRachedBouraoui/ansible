# ansible
ansible training
cmds:
	- ansible all -m apt -a "upgrade=dist" --become --ask-become-pass
	- ansible all -m apt -a "name=tmux state=latest"
	- ansible-playbook install_apache.yml --ask-become-pass
