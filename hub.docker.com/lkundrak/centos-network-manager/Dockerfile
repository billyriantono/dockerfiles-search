# Run me with: "docker run --privileged -ti <image>"

FROM centos:centos7
MAINTAINER https://wiki.gnome.org/LubomirRintel

ENV container docker
VOLUME [ "/sys/fs/cgroup" ]
CMD ["/usr/sbin/init"]

# Pull in NetworkManager that's recent enough
# https://copr.fedoraproject.org/coprs/lkundrak/NetworkManager-stable/repo/epel-7/lkundrak-NetworkManager-stable-epel-7.repo
ADD lkundrak-NetworkManager-stable-epel-7.repo /etc/yum.repos.d/lkundrak-NetworkManager-stable-epel-7.repo
RUN yum -y install NetworkManager

# No idea why this is there...
RUN rm /etc/sysconfig/network-scripts/ifcfg-ens3

# Enable console login
RUN usermod --password '' root
RUN systemctl unmask console-getty.service
RUN mkdir -p /etc/systemd/system/default.target.wants
RUN ln -sf /usr/lib/systemd/system/console-getty.service /etc/systemd/system/default.target.wants/console-getty.service
