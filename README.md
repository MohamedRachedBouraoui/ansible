# vm 
 * add user to sudoers:
	cmds:
	- visudo
	- type_the_user_name ALL=(ALL) ALL
		=> rached ALL=(ALL) ALL this will add the user "rached" as a sudoer

 * guest additions
	cmds in the guest machine:
	- sudo apt update
	- sudo apt install -y build-essential linux-headers-$(uname -r)
	then insert the "Install guest additions CD Image" and run it using the autorun.sh script
 * ssh
	* install openssh-server in guest machines:
	cmd: sudo apt-get install openssh-server
	* Must make the manual initial connection to all guests "Are you sure you want to connect ==> Yes"
	* create an ssh key-pain with a passphrase for the normal user account in the host machine
	 cmd: ssh-keygen -t ed25519 -C "mrb default" # add a passphrase to this key for more security
	* create an ssh key-pain that is specific to ansible without a passphrase in the host machine
	 cmd: ssh-keygen -t ed25519 -C "ansible" # don't add a passphrase to this key so that ansible will be able to cnnect to guests without beeing blocked by the password
	* copy host machine's pub keys to the guest machines
	cmd:
	  - ssh-copy-id -i path_to_pub_key guet_user_name@guest_ip
	* add the following alias to .bashrc to cache the passphrase
	  alias sshadd='eval $(ssh-agent) && ssh-add'
 * hosts managment:
	cmd: 
	  - sudo nano /etc/hosts  
	  - add the vm ip  and a hostname
# ansible
ansible training
cmds:
	- ansible all -m apt -a "upgrade=dist" --become --ask-become-pass
	- ansible all -m apt -a "name=tmux state=latest"
	- ansible-playbook install_apache.yml --ask-become-pass
	- ansible all -m gather_facts | grep ansible_dist
	- sudo firewall-cmd --add-port=80/tcp # allow communication with the port 80 (i.e; httpd)
	- sudo systemctl start httpd # to start the httpd service
	- sudo systemctl status mariadb # to check the service's status
