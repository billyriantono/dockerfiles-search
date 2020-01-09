FROM centos/systemd

RUN yum -y install https://repo.saltstack.com/yum/redhat/salt-repo-latest-2.el7.noarch.rpm 
RUN yum -y install salt-master salt-ssh

#ADD master /etc/salt/master
#ADD master-minion /etc/salt/minion

RUN salt-run salt.cmd tls.create_self_signed_cert

RUN useradd -m saltdev
RUN echo saltdev | passwd --stdin saltdev

RUN echo 'tmpfs /run tmpfs rw,nosuid,nodev,mode=755 0 0' >> /etc/fstab
RUN chmod +x /etc/rc.d/rc.local
RUN yum -y install rsyslog wget anacron git python-pygit2 GitPython
RUN yum -y install perl perl-Net-SSLeay openssl perl-IO-Tty perl-Encode-Detect
RUN yum -y install https://repo.saltstack.com/py3/redhat/salt-py3-repo-latest-2.el7.noarch.rpm 
RUN yum -y groupinstall 'Development Tools'
RUN yum -y install centos-release-scl
RUN yum -y install rh-python36
RUN scl enable rh-python36 bash
WORKDIR /opt/rh/rh-python36/root/usr/bin/
RUN /opt/rh/rh-python36/root/usr/bin/pip install salt
RUN /opt/rh/rh-python36/root/usr/bin/pip install salt-ssh

RUN mkdir /srv/salt
VOLUME /srv/salt

