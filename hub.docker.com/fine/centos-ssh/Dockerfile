FROM centos:7.4.1708
MAINTAINER Fe
RUN yum -y install wget vi vim lrzsz zip unzip git
RUN rm -rf /etc/yum.repos.d/* 
RUN wget -O /etc/yum.repos.d/CentOS-Base.repo http://mirrors.aliyun.com/repo/Centos-7.repo
RUN yum clean all
RUN yum install -y openssh-server sudo wget curl telnet
RUN sed -i 's/UsePAM yes/UsePAM no/g' /etc/ssh/sshd_config
RUN useradd admin 
RUN echo "root:1234567890" | chpasswd 
RUN ssh-keygen -t ed25519 -f /etc/ssh/ssh_host_ed25519_key
RUN mkdir /var/run/sshd
EXPOSE 22
CMD ["/usr/sbin/sshd", "-D"]
