FROM centos:7

## Install EPEL repo, yum necessary packages for the build without docs, clean all caches
RUN yum -y install epel-release &&         \
    yum -y install --setopt=tsflags=nodocs \
                   redis                   \
                   &&                      \
    yum clean all

CMD /usr/bin/redis-server --protected-mode no
