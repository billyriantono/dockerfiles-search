#This is a base comment 
#Centos
#VERSION               0.0.1
FROM centos:latest 
MAINTAINER zam007 <zam254227751@gmail.com> 

#yum install Package 
RUN yum -y install net-tools 
RUN yum -y install iputils  iproute  man  vim-minimal  openssh-server  openssh-clients
RUN yum -y install python-setuptools  
RUN easy_install supervisor   

#set supervisor 
RUN mkdir -p /var/log/supervisor 
RUN echo -e "[supervisord]\nnodaemon=true\n\n;[program:sshd]\n;command=/usr/sbin/sshd -D  \n\n;[program:httpd]\n;command=/usr/sbin/httpd -D FOREGROUND\n;autorestart = true" >> /etc/supervisord.conf 

#set ENV 
ENV LANG en_US.UTF-8 
ENV LC_ALL en_US.UTF-8 

#run supervisor 
CMD ["/usr/bin/supervisord" , "-c" , "/etc/supervisord.conf"] 
