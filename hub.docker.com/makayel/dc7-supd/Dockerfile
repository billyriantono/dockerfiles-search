FROM centos:7.1.1503
MAINTAINER makayel <michaelhatoum@gmail.com>

######################################################################################################
# Packages
######################################################################################################
# Update OS
RUN yum -y --skip-broken update

# Fix
RUN yum -y install yum-plugin-ovl && yum clean all

# Fix systemd conflit
RUN yum -y swap fakesystemd systemd && yum clean all

# Install epel repository
RUN /bin/rpm -Uvh http://download.fedoraproject.org/pub/epel/6/i386/epel-release-6-8.noarch.rpm

# Activate yum.repos.d baseurl
RUN find /etc/yum.repos.d -type f -exec sed -i.bak "s/#baseurl/baseurl/g" {} \;

# Install packages
RUN yum -y install openssh-server openssh-clients wget tar bzip2 net-tools python-setuptools gcc gcc-c++ libffi-devel openssl-devel libsasl2-devel openldap-devel git sudo && yum clean all

######################################################################################################
# RPM Oracle JDK 8u60
######################################################################################################
# Download RPM Oracle JDK 8u60
RUN wget -P /tmp/docker/ http://mirror.its.sfu.ca/mirror/CentOS-Third-Party/NSG/common/x86_64/jdk-8u60-linux-x64.rpm

# Install Oracle JDK 8u60
RUN rpm -ivh /tmp/docker/jdk-8u60-linux-x64.rpm

# Setting JAVA_HOME
ENV JAVA_HOME /usr/java/jdk1.8.0_60/

# Setting JRE_HOME
ENV JRE_HOME /usr/java/jdk1.8.0_60/jre/

# Setting PATH
ENV PATH $JAVA_HOME/bin:$JRE_HOME/bin:$PATH

######################################################################################################
# Scala 2.10.1
######################################################################################################
# Download Scala 2.10.1
RUN wget -P /tmp/docker/ http://www.scala-lang.org/files/archive/scala-2.10.1.rpm

# Install Scala 2.10.1
RUN rpm -ivh /tmp/docker/scala-2.10.1.rpm

######################################################################################################
# SBT
######################################################################################################

RUN curl https://bintray.com/sbt/rpm/rpm | sudo tee /etc/yum.repos.d/bintray-sbt-rpm.repo

RUN yum -y install sbt

######################################################################################################
# Anaconda2 4.3.0
######################################################################################################
# Download Anaconda2 4.3.0
RUN wget -P /tmp/docker/ https://repo.continuum.io/archive/Anaconda2-4.3.0-Linux-x86_64.sh

# Install Anaconda2 4.3.0
RUN bash /tmp/docker/Anaconda2-4.3.0-Linux-x86_64.sh -b -p /opt/anaconda/

# Setting Anaconda2 home
ENV ANACONDA2_HOME /opt/anaconda/anaconda2

# Setting PATH
ENV PATH $ANACONDA2_HOME/bin:$PATH

######################################################################################################
# Python Virtualenv
######################################################################################################
RUN /opt/anaconda/bin/pip install virtualenv

######################################################################################################
# User
######################################################################################################
# Ansible
RUN useradd --create-home --shell /bin/bash ansible
RUN usermod -aG wheel ansible
RUN echo "ansible:ST6jcbYTb82k49K" | chpasswd

# Root
RUN echo "root:ST6jcbYTb82k49K" | chpasswd

######################################################################################################
# SSH
######################################################################################################
# Make ssh directories
RUN mkdir /root/.ssh
RUN mkdir /home/ansible/.ssh
RUN mkdir /var/run/sshd

# Create host keys
RUN ssh-keygen -b 2048 -t rsa -f /etc/ssh/ssh_host_rsa_key -q -N ''

# Tell ssh to not use ugly PAM
RUN sed -i 's/UsePAM\syes/UsePAM no/' /etc/ssh/sshd_config

# Enable root login
RUN sed -i 's/#PermitRootLogin yes/PermitRootLogin yes/' /etc/ssh/sshd_config

# Disable password authentication
RUN sed -i 's/PasswordAuthentication yes/PasswordAuthentication no/' /etc/ssh/sshd_config

# Disable GSSAPIAuthentication
RUN sed -i 's/GSSAPIAuthentication yes/GSSAPIAuthentication no/' /etc/ssh/sshd_config

# Disable DNS
RUN sed -i 's/#UseDNS yes/UseDNS no/' /etc/ssh/sshd_config

######################################################################################################
# Common
######################################################################################################
# Make the terminal prettier
RUN echo "HOST_IP=$(ifconfig  | grep 'inet ' | grep -v '127.0.0.1' | cut -d ' ' -f 10 | head -n 1 | awk '{ print $1}')" >> /etc/profile
RUN echo "export PS1='[\u@$HOST_IP] \W # '" >> /etc/profile

# Enable networking
RUN echo 'NETWORKING=yes' >> /etc/sysconfig/network

# Remove /tmp/docker/
RUN rm -rf /tmp/docker

# Create temporary directory
RUN mkdir /tmp/makayel

######################################################################################################
# Supervisord
######################################################################################################
# Install supervisord
RUN easy_install supervisor
RUN /usr/bin/echo_supervisord_conf > /etc/supervisord.conf
RUN mkdir -p /var/log/supervisor

# Make supervisor run in foreground
RUN sed -i -e "s/^nodaemon=false/nodaemon=true/" /etc/supervisord.conf

# Tell supervisor to include relative .ini files
RUN mkdir /etc/supervisord.d
RUN echo  >> /etc/supervisord.conf
RUN echo [include] >> /etc/supervisord.conf
RUN echo 'files = /etc/supervisord.d/*.ini' >> /etc/supervisord.conf

######################################################################################################
# Openssh-server
######################################################################################################
# Add sshd program to supervisord config
RUN echo [program:sshd] >> /etc/supervisord.d/ssh.ini
RUN echo 'command=/usr/sbin/sshd -D' >> /etc/supervisord.d/ssh.ini
RUN echo  >> /etc/supervisord.d/ssh.ini

######################################################################################################
# Expose
######################################################################################################
EXPOSE 22

######################################################################################################
# Start container
######################################################################################################
CMD ["/usr/bin/supervisord", "-c", "/etc/supervisord.conf"]