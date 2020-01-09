FROM sensimilla/docker-squidguard

MAINTAINER Francesco Ferrari <francescouk@hotmail.com>

RUN echo "root:squid" | chpasswd

RUN apt-get update && apt-get install -y openssh-server
RUN mkdir /var/run/sshd
RUN sed -i 's/PermitRootLogin without-password/PermitRootLogin yes/' /etc/ssh/sshd_config

ENV NOTVISIBLE "in users profile"
RUN echo "export VISIBLE=now" >> /etc/profile

EXPOSE 22
EXPOSE 3128

CMD /usr/sbin/squid3 && /usr/sbin/sshd -D
