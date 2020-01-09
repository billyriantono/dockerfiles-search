FROM docker.io/centos:latest

RUN getent group haclient >/dev/null || groupadd -r haclient
RUN getent passwd hacluster >/dev/null || useradd -r -g haclient -d /var/lib/heartbeat/cores/hacluster -s /sbin/nologin -c "cluster user" hacluster
RUN yum clean all
RUN yum groupinstall -y "Server with GUI" "Development"
RUN yum install -y nss-devel glib2-devel libtool-ltdl-devel libuuid-devel libxslt-devel bzip2-devel dbus-devel gnutls-devel groff systemd-devel python-devel docbook-style-xsl help2man pam-devel perl-TimeDate libaio-devel
RUN yum install -y OpenIPMI-devel asciidoc openhpi-devel
RUN yum install -y resource-agents
RUN yum install -y libqb libqb-devel ncurses ncurses-devel net-snmp-devel
RUN yum install -y openssl-devel lz4-devel lzo-devel lksctp-tools-devel libnl3-devel
RUN mkdir -p /root/git

