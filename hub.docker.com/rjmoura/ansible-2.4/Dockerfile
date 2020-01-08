FROM webdevops/ansible:centos-7
RUN yum update -y \
    && yum install -y \
    epel-release \
    git \
    net-tools \
    openssh-server \
    openssh-clients \
    passwd \
    && yum clean all
    
ADD ./start.sh /start.sh
RUN mkdir /var/run/sshd

RUN ssh-keygen -t rsa -f /etc/ssh/ssh_host_rsa_key -N '' 

RUN chmod 755 /start.sh
RUN ./start.sh
ENTRYPOINT ["/usr/sbin/sshd", "-D"]
EXPOSE 22
