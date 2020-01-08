FROM stackbrew/ubuntu:13.10
MAINTAINER Greg Stephens < greg [at] udon {dot} org>
ENV MYPASSWORD password
# make sure the package repository is up to date
RUN echo "deb http://archive.ubuntu.com/ubuntu saucy main universe" > /etc/apt/sources.list
RUN apt-get update && apt-get -y upgrade
# set root password
RUN echo "root:$MYPASSWORD" | chpasswd
# Install Supervisor to start multiple processes
RUN apt-get -y install python-pip python-dev supervisor
RUN mkdir -p /var/log/supervisor
RUN /bin/echo -e "[supervisord]\nnodaemon=true\n" >/etc/supervisord.conf
# Install OpenSSH
RUN apt-get -y install openssh-server
RUN mkdir /var/run/sshd
RUN /usr/sbin/sshd
RUN sed -i 's/.*session.*required.*pam_loginuid.so.*/session optional pam_loginuid.so/g' /etc/pam.d/sshd
RUN /bin/echo -e "LANG=\"en_US.UTF-8\"" > /etc/default/local
# Install Tomcat
RUN apt-get install -y tomcat7 tomcat7-docs tomcat7-admin
RUN chgrp -R tomcat7 /etc/tomcat7
RUN sed -i '/\/tomcat-users/s#.*#<role rolename="manager"/>\n<role rolename="manager-gui"/>\n<role rolename="manager-status"/>\n<role rolename="manager-script"/>\n<user username="root" password="$MYPASSWORD" roles="manager,manager-gui,manager-status,manager-script"/>\n</tomcat-users>#' /etc/tomcat7/tomcat-users.xml
RUN service tomcat7 restart
# Create startup.sh script to start tomcat service
RUN /bin/echo -e "#!/bin/bash\ndate > start.log\nservice tomcat7 start\n" > /root/start.sh
RUN chmod +x /root/start.sh
# Set commands to be executed (sshd & start.sh)
RUN /bin/echo -e "[program:sshd]\ndirectory=/usr/local\ncommand=/usr/sbin/sshd -D\nautostart=true\nautorestart=true\nredirect_stderr=true\n" >>/etc/supervisord.conf
# Expose to random ports
EXPOSE 22 8080
RUN /bin/echo -e "\n\n[program:start]\ndirectory=/root\ncommand=/root/start.sh\nautostart=true\nautorestart=false\nredirect_stderr=true\n" >>/etc/supervisord.conf
ENTRYPOINT ["/usr/bin/supervisord","-n"]