# dev-env-automated-setup
contains an ansible playbook to install jenkins, dokku, and deploy a sample app to test dokku installation

How to?

On the ansible management node:
1- Install ansible
2- Create a user called ansible with its password
3- Create /home/ansible folder if it doesn't exit
4- Add ssh private key to /home/ansible/.ssh (the public key should resides in the remote machine too for the connection to be established!)
5- Create a user called dokku with its password(dokku) in the remote machine
6- Cat /path/to/public_key.pub | ssh root@{Your_remote_machine_IP_address} "sudo tee -a ~dokku/.ssh/authorized_keys"
7- Create a hosts file with this content in ansible management node:
[dev_servers]

{Your_remote_machine_IP_address} ansible_user=root ansible_ssh_private_key_file=/home/ansible/.ssh/id_rsa

8-run the playbook using the command:
sudo ansible-playbook -i hosts install_jenkins_dokku.yml --ask-become-pass
it'll ask for the root's pwd. Enter it to continue.
at the last taks, it'll prompt for the dokku password on the remote machine. Please enter the password (dokku in our case)

