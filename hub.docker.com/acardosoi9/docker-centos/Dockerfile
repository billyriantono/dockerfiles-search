FROM centos:centos5.11

ENV I9CORP_PASSWD=Mudar123
ENV JENKINS_PASSWD=Mudar123

RUN rm -fr /etc/yum.repos.d/*.repo
RUN rpm --nosignature -i http://vault.centos.org/5.11/os/x86_64/CentOS/wget-1.11.4-3.el5_8.2.x86_64.rpm
RUN wget --no-check-certificate https://centos.i9corp.com.br/centos/RPM-GPG-KEY
RUN wget --no-check-certificate http://centos.i9corp.com.br/centos/RPMS/x86_64/repo-i9corp-1-0.x86_64.rpm
RUN wget --no-check-certificate http://centos.i9corp.com.br/centos/RPMS/x86_64/yum-utils-1.1.16-21.el5.centos.noarch.rpm
RUN rpm -ivh *.rpm
RUN rpm --import RPM-GPG-KEY
RUN rm -fr *.rpm
RUN rm -fr RPM-GPG-KEY
COPY ./tools/CentOS-Base.repo /etc/yum.repos.d/CentOS-Base.repo

RUN mkdir -p /etc/packages-rpm
RUN yumdownloader --resolve --destdir /etc/packages-rpm/ libselinux libselinux-utils
RUN rpm -Uvh --force /etc/packages-rpm/*.rpm
RUN rm -fr /etc/packages-rpm

RUN yum clean all
RUN yum update -y
RUN yum install -y openssh-server sudo dos2unix vim vim-X11 samba libxml2-devel cmake mlocate postgresql-devel valgrind freetds-devel freetds
RUN yum groupinstall -y 'Development Tools'

RUN mkdir /etc/i9corp
RUN mkdir /jenkins

RUN ln -s /usr/include/libxml2/libxml /usr/include/libxml

COPY ./tools/start-packages /usr/local/bin/start-packages
RUN chmod +x /usr/local/bin/start-packages
RUN dos2unix /usr/local/bin/start-packages

RUN cp /etc/samba/smb.conf /etc/samba/smb.conf.bkp
COPY  ./samba/smb.conf /etc/samba/smb.conf
RUN dos2unix /etc/samba/smb.conf

RUN cp /etc/sudoers /etc/sudoers.bkp
COPY  ./sudo/sudoers /etc/sudoers
RUN dos2unix /etc/sudoers

RUN useradd -ms /bin/bash i9corp && echo "i9corp:${I9CORP_PASSWD}" | chpasswd
# RUN echo "i9corp ALL=(ALL) NOPASSWD:ALL" >> /etc/sudoers

RUN useradd -ms /bin/bash jenkins && echo "jenkins:${JENKINS_PASSWD}" | chpasswd
RUN chown -R jenkins:jenkins /etc/i9corp
RUN chown -R jenkins:jenkins /jenkins
# RUN echo "jenkins ALL=(ALL) NOPASSWD:ALL" >> /etc/sudoers

VOLUME [ "/etc/i9corp" ]

#SHH
EXPOSE 22
#Samba
EXPOSE 137/udp
EXPOSE 138/udp
EXPOSE 139
EXPOSE 445

CMD ["/usr/local/bin/start-packages"]
