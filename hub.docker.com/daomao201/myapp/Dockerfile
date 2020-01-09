FROM centos
MAINTAINER James@server.example.com
RUN yum install passwd openssl openssh-server net-tools -y
RUN /usr/sbin/sshd-keygen -A
RUN echo 'redhat' | passwd --stdin root
EXPOSE 22
CMD ["/usr/sbin/sshd","-D"]
