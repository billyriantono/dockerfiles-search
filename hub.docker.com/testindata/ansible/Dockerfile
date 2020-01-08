FROM centos:7
ADD Centos-7.repo /etc/yum.repos.d/CentOS-Base.repo
RUN yum -y install epel-release  && \
    yum -y install ansible python-psutil python-lxml python-netaddr python-pip python-docutils bubblewrap bzip2 python-crypto openssh openssh-clients && \
    rm -rf /var/cache/yum
