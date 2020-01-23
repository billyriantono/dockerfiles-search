FROM tomcat:7-jre8

ENV ADMIN_PWD admin123

ADD settings.xml /usr/local/tomcat/conf/
ADD tomcat-users.xml /usr/local/tomcat/conf/
ADD changepwd.sh /usr/local/changepwd.sh

CMD cd /usr/local && ./changepwd.sh && catalina.sh run