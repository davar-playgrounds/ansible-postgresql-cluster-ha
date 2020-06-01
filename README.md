
Ansible playbook installed
==========================

#### The following versions are installed
    postgres = 10
    patroni = latest
    consul = 1.6.0
    haproxy = latest
    keepalived = latest
    consul-template = 0.25.0

### REQUIRED!
    1) Minimum number of nodes = 3
    2) RedHat 7 or CentOS 7 or Ubuntu >=16.04 or Debian 8

Variable settings
--------------
Change the variable in the host.ini file (inventory/hosts.ini)

    ---
    test-01.mycompany.loc priority_num=<weight> # to the example 100
    test-02.mycompany.loc priority_num=<weight> # to the example 200
    test-03.mycompany.loc priority_num=<weight> # to the example 300

Change the variable in the host.ini file (inventory/group_vars/all.yml)

    ---
    vip_address: <your vip address>       # to the example 192.168.100.100
    vrouter_id: <your virtual router id>  # to the example 45



change the vaiable in the patroni (roles/patroni/defaults/main.yml)
   
    ---
    # Setting yaml file
    # General recommendation to set the shared_buffers is as follows.
    #
    #    Below 2GB memory, set the value of shared_buffers to 20% of total system memory.
    #    
    #    Below 32GB memory, set the value of shared_buffers to 25% of total system memory.
    #            
    #    Above 32GB memory, set the value of shared_buffers to 8GB

    patroni_sb: <size_shared_memory> # to example 750MB 

Dependencies
------------

No dependency

Running playbook
----------------
    ansible-playbook -i inventory/hosts.ini install-pg-cluster.yml -v
  
[![asciicast](https://asciinema.org/a/L7NeOOHGQ47t1Lr8u2r41C6cG.svg)](https://asciinema.org/a/L7NeOOHGQ47t1Lr8u2r41C6cG)


After installing the playbook, you can go to the haproxy statistics page for vip
---------------------------------------------------------------------------------

![haproxy-stat](https://user-images.githubusercontent.com/16415691/83475035-24f05000-a496-11ea-8e91-56e15de8192d.png)

Author Information
------------------

Vatolin Alexey