# adamnicholson-rpi-cluster

Home RPi cluster management

## Requirements

* [Ansible](http://www.ansible.com/)

## Installation

Edit `hosts.ini` file with your own topology.

See ansible docs for what a hosts inventory file should look like.

Run any of the playbooks.

## Usage

### Adding new hosts to the network

New hosts need to first be assigned the correct static IP.

Edit `hosts` to have a hosts group for `newnodes` which looks something like this

    [newnodes]
    192.168.0.32 ansible_user=pi target_ip=192.168.0.102

..replacing `192.168.0.32` with whatever the *current* IP of the new host is
(which was automatically assigned by DHCP), and replacing `192.160.0.102` in
the above example to whatever you *want* static IP of the host to be.

Then run the networking playbook

    ansible-playbook playbooks/tasks/networking.yml -i hosts.ini

This will set a new static IP and reboot the server.

Wait about 2 minutes for the server to reboot and come back up on its
new IP.

Then add the new IP to the `picluster` block of `hosts`, and remove it from the 
`newnodes` block.

### Updating all hosts

TBC

### Playbooks

These are docs for the indivudal playbooks which can be ran manually
if you desire for some reason.

## Networking

To assign a static IP to a new host

### Shutdown

To shutdown all your RPis execute the following playbook:

    ansible-playbook playbooks/tasks/shutdown.yml -i hosts.ini

### Reboot

To shutdown all your RPis execute the following playbook:

    ansible-playbook playbooks/tasks/reboot.yml -i hosts.ini
