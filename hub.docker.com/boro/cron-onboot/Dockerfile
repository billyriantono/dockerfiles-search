FROM centos:7
MAINTAINER Boro <docker@bo.ro>

# install crontabs
RUN yum -y update
RUN yum -y install crontabs nano python MySQL-python net-tools initscripts

# install git v2
RUN yum -y install  https://centos7.iuscommunity.org/ius-release.rpm
RUN yum -y install  git2u-all

# fix: "TERM environment variable not set." error when entering the container with bash
RUN echo "export TERM=xterm" >> /etc/bash.bashrc

# change timezone to JST
RUN cp /usr/share/zoneinfo/America/Toronto /etc/localtime

# comment out PAM
RUN sed -i -e '/pam_loginuid.so/s/^/#/' /etc/pam.d/crond

RUN chmod 0644 /etc/crontab

# Add crontab setting
# # RUN echo '* * * * * root /path/to/your/command' >> /etc/crontab

ADD start.sh /start.sh
RUN chmod 0777 /start.sh
RUN sed -i -e 's/\r$//' /start.sh

CMD /start.sh
