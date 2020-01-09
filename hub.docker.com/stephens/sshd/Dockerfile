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
# Install OpenSSH & set values to work with Ubuntu 13.10
RUN apt-get -y install openssh-server
RUN mkdir /var/run/sshd
RUN /usr/sbin/sshd
RUN sed -i 's/.*session.*required.*pam_loginuid.so.*/session optional pam_loginuid.so/g' /etc/pam.d/sshd
RUN /bin/echo -e "LANG=\"en_US.UTF-8\"" > /etc/default/local
# Expose 22 to random ports
EXPOSE 22
# Setup supervisor to start openssh
RUN /bin/echo -e "[program:sshd]\ndirectory=/usr/local\ncommand=/usr/sbin/sshd -D\nautostart=true\nautorestart=true\nredirect_stderr=true\n" >>/etc/supervisord.conf
ENTRYPOINT ["/usr/bin/supervisord","-n"]