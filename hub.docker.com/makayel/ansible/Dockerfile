FROM makayel/openssh
MAINTAINER Michael Hatoum <michael@adaltas.com>

RUN yum -y install ansible

CMD ["/usr/bin/supervisord", "-c", "/etc/supervisord.conf"]
