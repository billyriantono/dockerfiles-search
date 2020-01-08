FROM centos
   
MAINTAINER scanales

RUN yum install -y openssh-server sudo  
RUN sed -i 's/UsePAM yes/UsePAM no/g' /etc/ssh/sshd_config  

RUN yum  install -y openssh-clients

RUN yum install -y unzip
   
RUN echo "root:root" | chpasswd  
RUN echo "root   ALL=(ALL)       ALL" >> /etc/sudoers

RUN ssh-keygen -t dsa -f /etc/ssh/ssh_host_dsa_key  
RUN ssh-keygen -t rsa -f /etc/ssh/ssh_host_rsa_key  
   
RUN mkdir /var/run/sshd  
  
EXPOSE 22  
EXPOSE 8101
EXPOSE 2181
EXPOSE 2888
EXPOSE 3888
EXPOSE 1099
EXPOSE 44444
EXPOSE 8181
EXPOSE 8443
EXPOSE 9080-9099

CMD ["/usr/sbin/sshd", "-D"]
