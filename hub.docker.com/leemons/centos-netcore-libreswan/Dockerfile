FROM centos:7
ENV container docker
RUN (cd /lib/systemd/system/sysinit.target.wants/; for i in *; do [ $i == \
systemd-tmpfiles-setup.service ] || rm -f $i; done); \
rm -f /lib/systemd/system/multi-user.target.wants/*;\
rm -f /etc/systemd/system/*.wants/*;\
rm -f /lib/systemd/system/local-fs.target.wants/*; \
rm -f /lib/systemd/system/sockets.target.wants/*udev*; \
rm -f /lib/systemd/system/sockets.target.wants/*initctl*; \
rm -f /lib/systemd/system/basic.target.wants/*;\
rm -f /lib/systemd/system/anaconda.target.wants/*;
VOLUME [ "/sys/fs/cgroup" ]
RUN rpm -Uvh https://packages.microsoft.com/config/rhel/7/packages-microsoft-prod.rpm; yum update; yum install -y  libunwind libicu; yum install -y  dotnet-hosting-2.0.6
RUN yum install -y aspnetcore-runtime-2.1
RUN yum update \
    && yum install -y \
        ca-certificates      
RUN yum -y install libreswan;  yum install -y sysvinit-tools; systemctl enable ipsec

EXPOSE 500
EXPOSE 4500
EXPOSE 50
EXPOSE 51

CMD ["/usr/sbin/init"]
