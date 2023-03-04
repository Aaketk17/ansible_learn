## Ansible

### Commands

#### `ansible all -m ping`

Command to Test the connection between the remote host and the ansible. This command will send a test command to the remote host and if the remote host responds it will return a success message and if there is any host fail to respond ansible will send you the failure message

`ansible` : This is the Ansible command-line tool that lets you execute Ansible commands and playbooks.

`all` : This is an Ansible inventory keyword that specifies all hosts in the inventory should be targeted by the command.

`-m ping` : This is an Ansible option that specifies that the "ping" module should be used to execute the command.

---

#### `ansible all -i inventory -m ping`

Same funcional command as above but the differnce is here we have defined the hosts in the file name called `inventory`. by using the keyword `all` ansible will test the connection with all the hosts mentioned in the inventory file otherwise if we want to check the connection with only one host we can define the particular host IP instead of `all` in the command. `ansible 3.137.201.240 -i inventory -m ping`

---

#### `ansible all -m gather_facts`

Ansible command that uses the `gather_facts` module to gather facts about all hosts in your inventory. Here's a breakdown of the command:

`ansible` : This is the Ansible command-line tool that lets you execute Ansible commands and playbooks.

`all` : This is an Ansible inventory keyword that specifies all hosts in the inventory should be targeted by the command.

`-m gather_facts` : This is an Ansible option that specifies that the gather_facts module should be used to gather information about the remote hosts.
When you run this command, Ansible will connect to each host in your inventory and gather information about the host using various modules such as setup and fact. The information gathered by the gather_facts module is stored in memory on the Ansible control node and can be used later in the playbook. The information gathered can include things like network interface details, operating system version, disk usage, and more.

The gather_facts module is often used at the beginning of an Ansible playbook to collect information about the hosts that will be used later in the playbook. For example, you might use the information gathered by gather_facts to determine which software packages to install, or which configuration files to update.

---

#### `ansible.cfg`

The ansible.cfg file is a configuration file used by Ansible to define various settings and options for executing Ansible commands and playbooks. The ansible.cfg file can be used to customize the behavior of Ansible, set default values for command-line options, and configure connection settings for remote hosts.

The ansible.cfg file is typically located in the project directory or in the home directory of the user executing Ansible. When executing an Ansible command or playbook, Ansible searches for the ansible.cfg file in the following locations, in order:

1. The current directory
2. The home directory of the user executing the command
3. /etc/ansible/ansible.cfg

Here are some examples of settings that can be configured in the ansible.cfg file:

- Default values for command-line options, such as the default inventory file to use or the default username to use for SSH connections.
- Connection settings for remote hosts, such as the SSH private key to use or the number of parallel connections to use when executing tasks.
- Custom module paths, so that Ansible can find custom modules located in non-standard directories.
- Custom plugin paths, so that Ansible can find custom plugins located in non-standard directories.

By modifying the ansible.cfg file, you can customize the behavior of Ansible to better suit your needs and simplify your workflows.

if we define inventory file in the ansible.cfg file then we dont need to give the inventory file while executing the command. we can directly use the command `ansible all -m ping` it will take the hosts defined in the inventory file.

---

#### `ansible all --list-hosts`

command to list all the host defined in the inventory file

---

#### `ansible all -m yum -a name=aws-docker`

Command to install the desired packages to all the defined hosts using the `yum` module. if its a ubuntu machine we can use `apt` module

---

#### `--become --ask-become-pass`

`--become` : This is an Ansible option that specifies that the command should be executed with elevated privileges, using the sudo command or another privilege escalation method.

`--ask-become-pass` : This is an Ansible option that specifies that the user should be prompted for the password for privilege escalation.

When you run this command, Ansible will connect to each host in your inventory and execute the apt module with the name parameter set to tmux. The apt module will use the appropriate package manager (apt-get, aptitude, or dpkg) to install the tmux package on each host.

The --become and --ask-become-pass options are used to run the command with elevated privileges. This is necessary to install packages on the remote hosts, which may require root or administrator privileges.

---

#### `ansible all -m yum -a update_only=true --become --become-ask-pass` and `ansible all -m apt -a update_cache=true --become --become-ask-pass`

to run sudo apt-update or sudo yum update

---

#### `ansible-playbook apache.ansible.yml`

Command to run the playbook named apache.ansible.yml also can add `--ask-become-pass` as well

---

#### `when: ansible_distribution in ["Debian", "Ubuntu", "Amazon"] and ansible_distribution_version == "2"`

particular play will run only if the OS distribution is Debian, Ubuntu or Amazon and if the version is 2

---

#### Using `package` and `variables` in the playbook

```
---
- hosts: all
  become: true
  tasks:
    - name: install apache and php
      package:
        name:
          - '{{apache_package}}'
          - '{{php_package}}'
        state: latest
        update_cache: yes

```

here instead of defining the package managers like `yum` `apt` as per the underlying OS, we can directly use the `package` module. It will manages packages on a target without specifying a package manager module (like ansible.builtin.yum, ansible.builtin.apt, …). Installs, upgrade and removes packages using the underlying OS package manager.

We need to set the variables in the `inventory` file

```
# Amazon Linux
18.221.134.179 apache_package=httpd php_package=php
52.15.166.135 apache_package=httpd php_package=php

# Ubuntu
18.191.200.89 apache_package=apache2 php_package=libapache2-mod-php

```

---
