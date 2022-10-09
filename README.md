# ansible
Simple Ansible Commands

## Ansible Inventory
The Ansible inventory file lists servers or computers that Ansible will manage. This follows a simple YAML format explained below:

    sql_db1 ansible_host=sql01.xyz.com ansible_connection=ssh ansible_user=root ansible_ssh_pass=Lin$Pass
    
The first part is the server alias. This is a friendly name that you can use to manage your server. In this case, it's sql_db1. To assign the server alias you need to use the ansible_host= command.

The next part is the actual server name.

After that we have the connection type. Here you can use ssh for Linux or winrm for Windows servers.

Next, we have the ansible_user - this is self explanitory

Finally, we have the password for the ansible user. For Linux servers this will be ansible_ssh_pass, and for Windows it will be ansible_password.

Groups of servers can be set using a friendly name as shown below:

    [server_group1]
    sql_db1
    sql_db1
    web_1
    
    [web_app_group1]
    web_1
    app2
    app3
    
You can also create groups of groups, you just include the groups in a group and specify :children in the title of the group of groups.

    [master_server_group:children]
    server_group1
    web_app_group1
    
## Ansible Playbooks

Playbooks provide a list of instructions for the servers that are managed by Ansible. The format is simple: You have a YAML dictionary with a name:, a host:, and then an order list called tasks: that specifes what you want the server to do. Example:

        -
            name: 'cat hostfile playbook'
            hosts: localhost
            tasks:
                -
                    name: 'Execute a cat command to display host file'
                    command: cat /etc/hosts
                    
