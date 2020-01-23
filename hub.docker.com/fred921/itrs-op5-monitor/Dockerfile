FROM centos/systemd
MAINTAINER "Robert Claesson" <rclaesson@itrsgroup.com>
ENV container docker

ARG OP5_MONITOR_SOFTWARE_URL=https://d2ubxhm80y3bwr.cloudfront.net/Downloads/op5_monitor_archive/Monitor8/Tarball/op5-monitor-8.0.9-x64.tar.gz
ENV OP5_MONITOR_SOFTWARE_URL=$OP5_MONITOR_SOFTWARE_URL

# Install systemd
RUN yum -y install systemd; yum clean all; \
(cd /lib/systemd/system/sysinit.target.wants/; for i in *; do [ $i == systemd-tmpfiles-setup.service ] || rm -f $i; done); \
rm -f /lib/systemd/system/multi-user.target.wants/*;\
rm -f /etc/systemd/system/*.wants/*;\
rm -f /lib/systemd/system/local-fs.target.wants/*; \
rm -f /lib/systemd/system/sockets.target.wants/*udev*; \
rm -f /lib/systemd/system/sockets.target.wants/*initctl*; \
rm -f /lib/systemd/system/basic.target.wants/*;\
rm -f /lib/systemd/system/anaconda.target.wants/*;
VOLUME ["/sys/fs/cgroup"]

# Install prerequisites
RUN yum -y install wget which openssh-server net-tools firewalld

# Expose ports that are required by OP5
EXPOSE 80 443 5666 15551 22 161/tcp 162/udp

# Set default root password
RUN echo "root:monitor" | chpasswd

# Prepare entrypoint that will install OP5 Monitor when building
COPY entrypoint.sh /root/entrypoint.sh
RUN chmod +x /root/entrypoint.sh

# Restart after installation
CMD ["/usr/sbin/init"]
