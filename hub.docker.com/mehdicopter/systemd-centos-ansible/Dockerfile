FROM centos:6
LABEL MAINTAINER="Mehdicopter contact@mahfoudi.me"

RUN yum install -y sudo \
  initscripts \
  && yum clean all
  
RUN useradd -m -G wheel ansible \
  && sed -i "s/^#\s*\(%wheel\s\+ALL=(ALL)\s\+NOPASSWD:\s\+ALL\)/\1/" /etc/sudoers

# Molecule leaves zombie agetty with 100% CPU load -- https://github.com/ansible/molecule/issues/1104
RUN sed -i "/start_udev/s/^/#/g" /etc/rc.d/rc.sysinit \
  && rm -f /etc/init/tty.conf

CMD ["/sbin/init"]
