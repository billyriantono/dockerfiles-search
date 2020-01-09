FROM registry.fedoraproject.org/fedora:29
MAINTAINER Florian Dubourg <fd@ingeteldata.fr>
ADD entrypoint.sh /dhcpd
RUN dnf install -y dhcp-server && dnf clean all && \
    chmod 755 /dhcpd
CMD ["/dhcpd", "-d", "--no-pid"]
