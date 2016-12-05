# ansible_ansiblespec_repo
ansible_ansiblespec_repo for testing ansible using test kitchen and ansiblespec.

This demonstrates using test-kitchen, ansible and ansiblespec to build and verify an apache server.

## ansible and apache are installed and configured on the same server.


## ansible and apache are installed and configured on separate servers.
  * Everything is done via ssh from the Ansible/Serverspec server so nothing is installed on the apache server.
  * In this demonstration both servers are centos 7 running like Amazon EC2, or a Docker Container as long as they are accessible via ssh.
  * You can take an image of the server after it is build and no comfiguration software is install on the apache Server.
  * this is using ansible in ssh connection mode to do remote configuration.

![test-kitchen, ansible and serverspec](https://github.com/neillturner/ansible_ansiblespec_repo/blob/master/kitchen-ansible.png "test-kitchen, ansible and serverspec")


## Workstation Software Installation

The first thing you need to do is install the test-kitchen environment on your workstation.
A useful link is: http://misheska.com/blog/2013/12/26/set-up-a-sane-ruby-cookbook-authoring-environment-for-chef/

The follow instructions are for Windows PC (it will be similar for Mac):

1. Download and install virtualbox from https://www.virtualbox.org/wiki/Downloads.
2. Download and install Vagrant from https://www.vagrantup.com/downloads.html
3. Download and install the Windows RubyInstaller for 64 bit Ruby 2.1 from http://rubyinstaller.org/downloads.
   * Check the option to add ruby to your path.
4. Download and install the Windows Ruby DevKit for use with Ruby 2.0 and above (64bits version only) from http://rubyinstaller.org/downloads.
5. Configure the Ruby DevKit
   * In the devkit directory run “ruby dk.rb init”.
   * Check the config.yml generated has added the the path of the ruby install, if not add it manaully.
   * run “ruby dk.rb install” to bind it to the ruby installation.
6. Then install the following gems
  * gem install test-kitchen
  * gem install kitchen-ansible
  * gem install kitchen-verifier-serverspec
7. git clone the repository https://github.com/neillturner/ansible_ansiblespec_repo and in a command window in the ansible_ansiblespec_repo directory run command
```
kitchen list
```
This will return a list if everything is correctly installed.

## ansible and apache are installed and configured on the same server.

1. Create 1 linux server for both ansible and apache using a keypair using say AWS Cloud Formation.
2. In ansible_ansiblespec_repo update the inventory/hosts_ssh with IP address of linux server.
3. In the .kitchen.yml file
   * Set the ssh_key  to the aws keypair for linux server e.g. spec/test.pem
   * Set the hostname to ip address of linux server  e.g.'54.229.103.38'
4. create, converge, verify and destroy the ansible-centos-70 server
```
kitchen create ansible-centos-70 -l debug
kitchen converge ansible-centos-70 -l debug
kitchen verify ansible-centos-70 -l debug
kitchen destroy ansible-centos-70 -l debug
```

## ansible and apache are installed and configured on separate servers.

1. Create 2 linux servers one for ansible and one for apache using a keypair using say AWS Cloud Formation.
2. In ansible_ansiblespec_repo update the inventory/hosts_ssh with IP address of apache server.
3. In the .kitchen.yml file
   * Set the ssh_key  to the aws keypair for ansible and apache server e.g. spec/test.pem
   * Set the hostname to ip address of ansible server  e.g.'54.229.103.38'
4. create, converge, verify and destroy the ansible-centos-70 server
```
kitchen create ansible-centos-70 -l debug
kitchen converge ansible-centos-70 -l debug
kitchen verify ansible-centos-70 -l debug
kitchen destroy ansible-centos-70 -l debug
```






