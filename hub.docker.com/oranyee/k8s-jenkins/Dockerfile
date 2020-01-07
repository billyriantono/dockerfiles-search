FROM jenkins/jenkins:lts
MAINTAINER YiXin xin.yi@ncsi.com.cn

RUN /usr/local/bin/install-plugins.sh ansicolor
RUN /usr/local/bin/install-plugins.sh greenballs

RUN /usr/local/bin/install-plugins.sh kubernetes

USER jenkins
