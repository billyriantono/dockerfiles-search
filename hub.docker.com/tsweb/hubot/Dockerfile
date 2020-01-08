FROM tsweb/centos64
MAINTAINER Kazuhisa Kumagai <k-kumagai@ts.tv-osaka.co.jp>

#--------------------------------------
# install Hubot
#--------------------------------------

RUN rpm -ivh http://ftp.jaist.ac.jp/pub/Linux/Fedora/epel/6/x86_64/epel-release-6-8.noarch.rpm
RUN yum install -y --enablerepo=centosplus npm
RUN yum install -y redis

RUN npm install -g coffee-script hubot@2.8.3
RUN hubot --create /root/hubot
RUN cd /root/hubot && npm install

# install script: jenkins, jenkins-notifier
RUN cd /root/hubot &&\
	cp node_modules/hubot-scripts/src/scripts/jenkins.coffee scripts &&\
	cp node_modules/hubot-scripts/src/scripts/jenkins-notifier.coffee scripts
ENV HUBOT_JENKINS_URL http://jenkins:8080

#--------------------------------------
# initialize
#--------------------------------------

ADD supervisor.conf /etc/supervisord/conf/service.conf
CMD ["/usr/bin/supervisord"]
