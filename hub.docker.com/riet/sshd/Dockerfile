FROM centos:7.2.1511
MAINTAINER riet
RUN yum install -y epel-release && yum install -y openssh-server passwd
RUN echo "@WSX3edc" | passwd --stdin root && \
    sed -i "s/#UseDNS yes/UseDNS no/" /etc/ssh/sshd_config && \
    ssh-keygen -t rsa -f /etc/ssh/ssh_host_rsa_key && \
    ssh-keygen -t dsa  -f /etc/ssh/ssh_host_dsa_key && \
    ssh-keygen -t ecdsa -f /etc/ssh/ssh_host_ecdsa_key && \
    ssh-keygen -t dsa -f /etc/ssh/ssh_host_ed25519_key && \
    cp -f /usr/share/zoneinfo/Asia/Shanghai /etc/localtime
EXPOSE 22
CMD ["/usr/sbin/sshd", "-D"]
