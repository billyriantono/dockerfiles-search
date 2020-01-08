FROM sigtom/docker-cent6base
MAINTAINER "Tommy Craddock" <tec.thor@gmail.com>
RUN yum -y install nano wget mlocate telnet openssh-server.x86_64 openssh-clients.x86_64; yum clean all; service sshd start
RUN yum -y update
EXPOSE 22
CMD ["/bin/bash"]
