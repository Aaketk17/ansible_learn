## Ansible

### Commands

#### ```ansible all -m ping```

Command to Test the connection between the remote host and the ansible. This command will send a test command to the remote host and if the remote host responds it will return a success message and if there is any host fail to respond ansible will send you the failure message

```ansible```  :   This is the Ansible command-line tool that lets you execute Ansible commands and playbooks.

```all```      :   This is an Ansible inventory keyword that specifies all hosts in the inventory should be targeted by the command.

```-m ping```  :   This is an Ansible option that specifies that the "ping" module should be used to execute the command.

-----------------------------------------------------------------------------------------------------------------------------------------------------------

#### ```ansible all -i inventory -m ping```

Same funcional command as above but the differnce is here we have defined the hosts in the file name called ```inventory```. by using the keyword ```all``` ansible will test the connection with all the hosts mentioned in the inventory file otherwise if we want to check the connection with only one host we can define the particular host IP instead of ```all``` in the command. ```ansible 3.137.201.240 -i inventory -m ping```

-----------------------------------------------------------------------------------------------------------------------------------------------------------

#### ```ansible all -m gather_facts```

Ansible command that uses the ```gather_facts``` module to gather facts about all hosts in your inventory. Here's a breakdown of the command:

```ansible``` : This is the Ansible command-line tool that lets you execute Ansible commands and playbooks.

```all``` : This is an Ansible inventory keyword that specifies all hosts in the inventory should be targeted by the command.

```-m gather_facts``` : This is an Ansible option that specifies that the gather_facts module should be used to gather information about the remote hosts.
When you run this command, Ansible will connect to each host in your inventory and gather information about the host using various modules such as setup and fact. The information gathered by the gather_facts module is stored in memory on the Ansible control node and can be used later in the playbook. The information gathered can include things like network interface details, operating system version, disk usage, and more.

The gather_facts module is often used at the beginning of an Ansible playbook to collect information about the hosts that will be used later in the playbook. For example, you might use the information gathered by gather_facts to determine which software packages to install, or which configuration files to update.

-----------------------------------------------------------------------------------------------------------------------------------------------------------

