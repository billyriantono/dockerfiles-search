FROM fedora

MAINTAINER Mohamed Ashiq Liyazudeen <mliyazud@redhat.com>

LABEL Name="glusterfs-client"

ENV container docker

RUN dnf --setopt=tsflags=nodocs -y update; dnf clean all; dnf --setopt=tsflags=nodocs -y install wget nfs-utils attr iputils iproute;

RUN wget http://download.gluster.org/pub/gluster/glusterfs/3.7/LATEST/Fedora/glusterfs-fedora.repo -O /etc/yum.repos.d/glusterfs-fedora.repo

RUN sed -i "s/LANG/\#LANG/g" /etc/locale.conf

RUN dnf install -y glusterfs-fuse; dnf clean all;

CMD ["/bin/bash"]
