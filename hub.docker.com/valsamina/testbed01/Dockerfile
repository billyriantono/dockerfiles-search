FROM centos:centos6

# epel
RUN rpm -ivh --nosignature http://dl.fedoraproject.org/pub/epel/6/x86_64/epel-release-6-8.noarch.rpm

# remi
RUN rpm -ivh --nosignature http://rpms.famillecollet.com/enterprise/remi-release-6.rpm

# rpmforge
RUN rpm -ivh --nosignature http://pkgs.repoforge.org/rpmforge-release/rpmforge-release-0.5.3-1.el6.rf.x86_64.rpm

RUN yum install -y sudo passwd wget tar autoconf make gcc gcc-c++


ADD testbed01.txt /testbed01.txt

CMD tail -f /dev/null
