FROM arnow117/ubuntu_base:latest

MAINTAINER arnow117 "arnow117@gmail.com"

#Config default sshd
RUN mkdir /var/run/sshd
RUN echo 'root:root' |chpasswd
RUN sed -ri 's/^PermitRootLogin\s+.*/PermitRootLogin yes/' /etc/ssh/sshd_config
RUN sed -ri 's/UsePAM yes/#UsePAM yes/g' /etc/ssh/sshd_config
EXPOSE 22/tcp
CMD ["/usr/sbin/sshd","-D"]

WORKDIR $WORK_PATH