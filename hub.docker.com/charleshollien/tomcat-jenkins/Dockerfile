FROM oraclelinux:7
RUN yum install wget openssh-clients git -y && yum install --enablerepo=ol7_addons tomcat docker sudo python-setuptools -y
RUN easy_install pip && pip install ansible
RUN wget http://mirrors.jenkins.io/war-stable/latest/jenkins.war -O /var/lib/tomcat/webapps/ROOT.war
#VOLUME /usr/share/tomcat
RUN usermod -aG dockerroot tomcat
RUN echo "tomcat ALL=(ALL) NOPASSWD: ALL" > /etc/sudoers.d/tomcat
USER tomcat
CMD /usr/libexec/tomcat/server start
