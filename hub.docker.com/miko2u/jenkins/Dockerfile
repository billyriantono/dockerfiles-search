FROM miko2u/centos6
MAINTAINER miko@cafelounge.net

# packages
RUN cd /etc/yum.repos.d \
 && curl -OL http://pkg.jenkins-ci.org/redhat/jenkins.repo \
 && rpm --import http://pkg.jenkins-ci.org/redhat/jenkins-ci.org.key \
 && yum -y update \
 && yum -y install java-1.8.0-openjdk jenkins subversion git \
 && yum clean all \
 && find / -group jenkins | xargs chgrp 467; groupmod -g 467 jenkins \
 && find / -user jenkins | xargs chown 467; usermod -u 467 jenkins

# bootstrap
ADD boot/* /boot/

# expose
EXPOSE 8080
