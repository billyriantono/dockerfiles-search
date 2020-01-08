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

RUN yum -y update && \
    yum -y install epel-release && \
    yum -y install http://opensource.wandisco.com/centos/7/git/x86_64/wandisco-git-release-7-2.noarch.rpm && \
    yum -y install epel-release gdisk sudo curl gzip jq parted git make ansible python python-six python-yaml python-requests rpm-build

RUN yum -y install python-configobj python-oauthlib python-jsonschema python-jsonpatch e2fsprogs iproute net-tools rsyslog && \
    yum -y install python-devel python-nose python-httpretty python-mock python-unittest2 python-contextlib2 python-coverage python-tox python-pip

VOLUME [ "/sys/fs/cgroup" ]

# install azure cli
RUN rpm --import https://packages.microsoft.com/keys/microsoft.asc && \
    echo -e "[azure-cli]\nname=Azure CLI\nbaseurl=https://packages.microsoft.com/yumrepos/azure-cli\nenabled=1\ngpgcheck=1\ngpgkey=https://packages.microsoft.com/keys/microsoft.asc" > /etc/yum.repos.d/azure-cli.repo && \
    yum -y install azure-cli

# install python kusto sdk
RUN pip install azure-kusto-data && \
    pip install azure-kusto-ingest

CMD ["/usr/sbin/init"]
