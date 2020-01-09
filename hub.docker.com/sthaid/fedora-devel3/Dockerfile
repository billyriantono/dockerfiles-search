FROM fedora

MAINTAINER sthaid <stevenhaid@gmail.com>

RUN yum install -y openssh-server openssh-clients passwd net-tools
RUN yum groupinstall -y "development tools"
RUN yum clean all
RUN ssh-keygen -A
RUN useradd user
RUN echo -e "password\npassword" | (passwd --stdin user)

ENTRYPOINT ["/usr/sbin/sshd", "-D"]

