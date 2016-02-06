# duplo-building-blocks


I like to think of Vagrant as being the Duplo of building blocks, and then AWS/OpenStack the Legos of building blocks.


What this repo provides is:
  Load Balancers:
    HAProxy and Keepalived
  Web Servers:
    NGINX and Tomcat
  Database Servers:
    MySQL
  Configuration Management:
    Ansible
Pretty much the basics for any Highly Available Cloud Application in a nice local lab environment driven by Ansible.


Testing
  http://192.168.56.70:8181/                        # HAProxy stats
  http://192.168.56.70/                             # NGINX web service
  http://192.168.56.70:8080/mysql-sample/           # Tomcat app with a MySQL backend


Notes
  I like to use VirtualBox Host-Only Network on eth1 and then NAT network on eth0
  I find this always allow access to your instances on your desired ports and address scheme
  While still allowing outbound internet access with no external attack surface

Enhancements
  As with most projects, there is always more to do.  Things I plan on doing include:
    MySQL HA and MongoDB cluster
    SSH Key Management/Cleanup/Scanning
    More dynamic inventories and services
    A much better README