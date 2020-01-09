FROM clouder/clouder-base
MAINTAINER Yannick Buron yburon@goclouder.net

RUN touch /tmp/odoo-ssh
RUN apt-get -qq update && DEBIAN_FRONTEND=noninteractive apt-get -y -qq install openssh-server
RUN mkdir /var/run/sshd
RUN chmod 0755 /var/run/sshd
USER root

CMD /usr/sbin/sshd -ddd
