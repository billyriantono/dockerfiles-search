FROM jschueths/supervisord

MAINTAINER Josh Schueths <jschueths@gmail.com>

RUN apt-get update
RUN apt-get install -y openssh-server
RUN echo "root:rootpassword" | chpasswd
RUN sed -i 's/PermitRootLogin without-password/PermitRootLogin yes/g' /etc/ssh/sshd_config
RUN mkdir -p /var/run/sshd

EXPOSE 22

ADD sshd.conf /etc/supervisor/conf.d/sshd.conf

# No cmd or entrypoint since it's defined in jschueths/supervisord

