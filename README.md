#Set up ansible with multiple hosts using containers as your hosts servers
#Definition
Ansible is an open source IT automation tool. It helps in managing configuration, running playbooks for continuous deployments, basically streamlining the deployment, and orchestrating different environments.

#Prerequisites

- Create an AWS EC2 instance (Using ubuntu, open a ssh port ( port 22) )
- Conect remotely to this AWS EC2 instance ( you must be in the directory where your aws EC2 key pair is located)
- Run a command to updating and upgrading linux packages

  $ sudo apt-get update | sudo apt-get upgrade -y

- Install docker

  $ sudo apt-get install docker.io -y

- Give ubuntu user permission to run a docker command as administrator

  $ sudo usermod -aG docker ubuntu

- log out and log back in for your changes to take efec with the "exit" command and reconnect remotely

  $ exit

1. Download Ansible image in Dockerhub repository (akloud12)

  $ docker pull akloud12/ubuntu-ansible

2. Running a (07) container On this Instance.

 - One container for our Ansible server
 - Six container for our ansible agent
 
  $ docker run -itd akloud12/ubuntu-ansible

- We're Using : 
 . d : Is to run the container in Detach mode, meaning the container runs in the backgrand you get your promt 
 . i : inter-active mode 
 . t : terminal
run this command 6 more times to have to have a total of 7 servers.
 $ docker run -itd akloud12/ubuntu-ansible

3. Login to your Ansible server

 $ docker exec -it <<ansible_server_container_name>> type_of_shell (bash shell, Korn shell,c shell )

4. Check to know if the necessary tools (Ansible, git) are installed and also checking the configuration files

- Checking Ansible :

 $ ansible --version

- Checking git :

 $ git --version

- Checking the configuration file ( /etc/ansible/)

 $ ls /etc/ansible/
    To list our configuration files

 $ cat /etc/ansible/ansible.cfg

 $ cat /etc/ansible/hosts

5. Clone a ansible repository from github (akdevops12)

 $ git clone https://github.com/akdevops12/ansible.git

6. Cd in your ansible directory

 $ cd ansible/
 
7. copy the "hosts" file to our ansible directory and replace the other one existing in ansible configuration file. To have our hosts file configure to Set up ansible with multiple hosts.

$ cp hosts /etc/ansible/

8. Disable Host Key Checking in the configuration file by removing the (#).

 $ vim /etc/ansible/ansible.cfg

Uncomment the line : 
#host_key_checking = false

to

host_key_checking = false

To search a specific line of a file in vi, we can go to exec mode, Then type / follow by the word that you are looking for.

for example : look for "host_key_checking"

/host_key_checking

9. Test a connectivity between our ansible server and all the ansible agents

 $ ansible all -m ping

 . all : is to attach all of your target servers 
 . m : is for module. In this case the module is ping 
 . ping : type of module use to test a connectivity between your ansible server and your target servers.
