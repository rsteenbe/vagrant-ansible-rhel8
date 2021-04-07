# Vagrant Box with Ansible and RHEL8 target servers

Two machines will be running after running the command:
`vagrant up`

The first machine is the Ansible machine where you can make a connection through SSH:
`vagrant ssh ansible`

The second machine is an empty machine where you can make a connection through SSH:
`vagrant ssh server1`

After running `vagrant ssh ansible` you can SSH to the empty machine:
`ssh 192.168.50.10`

Username:
`vagrant`

Password:
`vagrant`

# Running a playbook
SSH to the Ansible machine:
`vagrant ssh ansible`

Execute the playbook:
`ansible-playbook -i /vagrant/hosts /vagrant/apache.yml`
