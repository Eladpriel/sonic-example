# sonic-examples


setting up the control node

1. setup Python 3 enviorment
	sudo -i
	cd /usr/bin
	ln -fs python3 python
	python --veriosn

2.  performthe Requied APT update
	apt update
	apt -y upgrade
	apt install - y python3-pip sshpass

3. Perform your pip3 installs
	pip3 install paramiko
	pip3 install ansible-base
	Validate the corrcect versions pip3 list | grep –iE ‘Cryptography|jinja2|Paramiko|Ansible-base’
	ansible --version
	
4. Install Enterprise SONiC Collection and verify Collection Inventory in your Ansible Control Machine
	echo "collection_paths = /usr/share/ansible/collections“ >> /etc/ansible/ansible.cfg
	ansible-galaxy collection install dellemc.enterprise_sonic
	ansible-galaxy collection list
	
5. Setup your Ansible Environment. 
	mkdir /etc/ansible
	echo "[defaults]" > /etc/ansible/ansible.cfg
  echo "host_key_checking = False" >> /etc/ansible/ansible.cfg
  echo "interpreter_python = auto" >> /etc/ansible/ansible.cfg

6. Test ping loopback and other hosts with paramiko using Ansible one-liners
	ansible all -i 127.0.0.1, -u sonicdemo -k -m ping
  ansible all -i 172.17.112.9, -c paramiko -u admin -k -m ping

7. Try a basic command to verify that Ansible can reach the switches. Replace the IP addresses and credentials per your case
  ansible all -i 172.17.112.8,172.17.112.9 -c network_cli -e "ansible_network_os=dellemc.enterprise_sonic.sonic ansible_ssh_user=admin ansible_ssh_pass=sonicdemo“ -m dellemc.enterprise_sonic.sonic_command -a "commands='show version | grep Software’”

8. Enterprise Sonic Collection Directory Default Path (in this order)
	(current_playbooks)/collections
	~/.ansible/collections
	/usr/share/ansible/collections/ansible_collections/dellemc/enterprise_sonic/












	

	 


