FROM centos:7
MAINTAINER miko@cafelounge.net

# networking & timezone && user
RUN cd /tmp \
 && yum -y update \
 && yum -y install epel-release \
 && yum -y install rpmdevtools \
        rpm-build yum-utils gcc gcc-c++ gcc-gfortran intltool libtool \
        autoconf automake make cmake tar rsync gnupg2 createrepo systemtap \
 && yum clean all \
 && rm -rf /tmp/* /var/tmp/* /var/lib/yum/* /var/cache/yum/* \
 && mkdir -p /root/rpmbuild/{RPMS/x86_64,RPMS/noarch,SOURCES,SPECS,SRPMS}

# entrypoint
COPY init /boot/
ENTRYPOINT ["/boot/init"]
