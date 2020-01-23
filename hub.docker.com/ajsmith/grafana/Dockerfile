FROM fedora:24

MAINTAINER Alex Smith <alex.smith@redhat.com>

ADD common/setup.sh /tmp/setup.sh
RUN /bin/bash /tmp/setup.sh
ADD grafana.repo /etc/yum.repos.d/grafana.repo
ADD fedora/install_packages.sh /tmp/install_packages.sh
RUN /bin/bash /tmp/install_packages.sh
ADD grafana.ini /etc/grafana/grafana.ini

EXPOSE 3000

VOLUME ["/var/lib/grafana"]
VOLUME ["/var/log/grafana"]
VOLUME ["/etc/grafana"]

USER grafana

CMD ["/usr/sbin/grafana-server", "-config", "/etc/grafana/grafana.ini", "-homepath", "/usr/share/grafana", "-pidfile", "/var/run/grafana/grafana.pid"]
