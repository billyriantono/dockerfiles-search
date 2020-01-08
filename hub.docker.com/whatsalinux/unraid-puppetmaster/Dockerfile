FROM centos:7
MAINTAINER dimitrius@gmail.com
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
CMD ["/usr/sbin/init"]
RUN groupadd -g 994 puppet

## setup yum
RUN /bin/rm -f /etc/yum.repos.d/epel* && yum clean all
COPY configs/fastestmirror.conf /etc/yum/pluginconf.d
RUN yum -y install https://yum.puppet.com/puppet5-release-el-7.noarch.rpm
RUN yum -y install http://dl.fedoraproject.org/pub/epel/epel-release-latest-7.noarch.rpm
RUN yum -y install https://yum.theforeman.org/releases/1.22/el7/x86_64/foreman-release.rpm
RUN yum -y install http://dl.fedoraproject.org/pub/epel/epel-release-latest-7.noarch.rpm || :
RUN sed -i 's/gpgcheck=1/gpgcheck=0/g' /etc/yum.repos.d/* && yum clean all && yum makecache fast
RUN yum install -y yum-utils
RUN yum-config-manager --enable centosplus >& /dev/null
RUN yum-config-manager --enable rhel-7-server-optional-rpms rhel-server-rhscl-7-rpms

## install packages
RUN yum install -y vim \
git \
perl \
openssh-clients \
bash-completion-extras \
mariadb \
bind-utils \
mlocate \
cmake \
gnulib-devel \
libcurl-devel \
openssl-devel \
man-db \
rsyslog \
mailx \
sendmail \
sendmail-cf \
puppet-agent \
foreman-installer

## install oracle java
COPY configs/jdk-8u221-linux-x64.rpm /etc/jdk-8u221-linux-x64.rpm
RUN yum localinstall -y /etc/jdk-8u221-linux-x64.rpm
ENV JAVA_HOME /usr/java/latest
ENV PATH $JAVA_HOME/bin:$PATH
RUN echo -e "export JAVA_HOME=/usr/java/latest\nexport PATH=\$JAVA_HOME/bin:\$PATH" > /etc/profile.d/java_home.sh && chmod 644 /etc/profile.d/java_home.sh && /bin/rm -f /etc/jdk-8u221-linux-x64.rpm

## for sending mail
RUN ln -s /bin/mailx /bin/email
COPY configs/mail.rc /etc/mail.rc
COPY configs/configs.tar /etc/configs.tar

## copy foreman installer file
COPY configs/foreman-answers.yaml /etc/foreman-installer/scenarios.d/foreman-answers.yaml
RUN chmod 600 /etc/foreman-installer/scenarios.d/foreman-answers.yaml

## clean up yum
RUN yum clean all

## some puppet housekeeping
RUN mkdir -p puppetlabs/r10k

## add a firstrun script (will only run on first boot)
COPY configs/first_start_setup.sh /usr/local/bin/first_start_setup
RUN chmod +x /usr/local/bin/first_start_setup
RUN ln -s /usr/local/bin/first_start_setup /root/first_start_setup.sh

EXPOSE 8140 443 8444 80
