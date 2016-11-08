# duplo-building-blocks

This is just a fun little repo I built for myself to improve upon foundational skills.

### What's in the Repo?
  - Load Balancer:
    - HAProxy
    - Keepalived
  - Web Servers:
    - Apache
    - NGINX
    - Tomcat
  - Database Servers:
    - MySQL
  - Service Assurance
    - Nagios
    - ELK
  - Configuration Management:
    - Ansible

### Testing
  - http://192.168.56.70:8181/                        # HAProxy stats
  - http://192.168.56.70/                             # NGINX web service
  - http://192.168.56.70:8080/mysql-sample/           # Tomcat app with a MySQL backend
  - http://192.168.56.70:8081/                        # Apache site with basic auth
  - http://192.168.56.80/nagios/                      # Nagios web service
