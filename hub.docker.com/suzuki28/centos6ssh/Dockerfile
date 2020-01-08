# centos6
FROM centos:6

RUN yum -y install initscripts MAKEDEV
RUN yum check
RUN yum -y update

# install for DevEnv
RUN yum install -y sudo passwd openssh openssh-clients openssh-server httpd vim python-setuptools
RUN yum install -y gcc make gcc-c++ zlib-devel httpd-devel openssl-devel curl-devel sqlite-devel
# install for supervisord
RUN easy_install supervisor

# install for iseconv
# ADD ./iseconv-3.0-1.0.x86_64.rpm /iseconv-3.0-1.0.x86_64.rpm
# RUN rpm -ivh /iseconv-3.0-1.0.x86_64.rpm

# install for serf
RUN yum -y install wget unzip
RUN wget -O 0.6.4_linux_amd64.zip https://dl.bintray.com/mitchellh/serf/0.6.4_linux_amd64.zip
RUN unzip -d /usr/sbin 0.6.4_linux_amd64.zip
RUN chmod 775 /usr/sbin/serf

# configuration for sshd
RUN sed -ri 's/UsePAM yes/#UsePAM yes/g' /etc/ssh/sshd_config
RUN sed -ri 's/#UsePAM no/UsePAM no/g' /etc/ssh/sshd_config
# gen for ssh-key
RUN ssh-keygen -t rsa -f /etc/ssh/ssh_host_rsa_key
RUN ssh-keygen -t dsa -f /etc/ssh/ssh_host_dsa_key
# creation of ssh user
RUN echo 'root:rootpassw0rd' | chpasswd
RUN useradd user01
RUN echo 'user01:passw0rd' | chpasswd
RUN echo 'user01 ALL=(ALL) NOPASSWD:ALL' >> /etc/sudoers.d/user01
# for session down
RUN echo 'ClientAliveInterval 300' >> /etc/ssh/sshd_config

# Top page for WEB
RUN echo '404 error:The page was deleted or does not exist.' > /var/www/html/index.html

# configuration for supervisord
RUN touch /etc/supervisord.conf
RUN echo '[supervisord]'  >> /etc/supervisord.conf
RUN echo 'nodaemon=true'  >> /etc/supervisord.conf

RUN echo '[program:sshd]'             >> /etc/supervisord.conf
RUN echo 'command=/usr/sbin/sshd -D' >> /etc/supervisord.conf
RUN echo 'autostart=true' >> /etc/supervisord.conf
RUN echo 'autorestart=true' >> /etc/supervisord.conf

RUN echo '[program:httpd]' >> /etc/supervisord.conf
RUN echo 'command=/usr/sbin/httpd -c "ErrorLog /dev/stdout" -DFOREGROUND' >> /etc/supervisord.conf
RUN echo 'redirect_stderr=true' >> /etc/supervisord.conf

RUN echo '[program:serf]' >> /etc/supervisord.conf
RUN echo 'command=/usr/sbin/serf agent -discover=isespd01 -event-handler=query:sh=/bin/bash' >> /etc/supervisord.conf

# port
EXPOSE 22 80

# supervisord and param
ENTRYPOINT ["/usr/bin/supervisord"]
CMD ["-c", "/etc/supervisord.conf"]
