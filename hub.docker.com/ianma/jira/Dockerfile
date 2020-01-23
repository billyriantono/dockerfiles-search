FROM ubuntu:16.04

RUN apt-get update && \
		apt-get install wget -y && \
		wget https://s3.cn-northwest-1.amazonaws.com.cn/public-files/jdk-8u172-linux-x64.tar.gz && \
		tar xzf jdk-8u172-linux-x64.tar.gz -C /usr/local && \
		mkdir -pv /var/jira /opt && \
		wget https://s3.cn-northwest-1.amazonaws.com.cn/public-files/atlassian-jira-software-7.2.2.tar.gz && \
		tar xzf atlassian-jira-software-7.2.2.tar.gz -C /opt && \
		mv /opt/atlassian-jira-software-7.2.2-standalone /opt/jira &&\
		rm atlassian-jira-software-7.2.2.tar.gz
COPY mysql-connector-java-5.1.39-bin.jar /opt/jira/atlassian-jira/WEB-INF/lib/
COPY atlassian-extras-3.1.2.jar /opt/jira/atlassian-jira/WEB-INF/lib/
ENV JAVA_HOME /usr/local/jdk1.8.0_172
ENV PATH $JAVA_HOME/bin:$PATH
ENV JRE_HOME $JAVA_HOME/jre
ENV CLASSPATH $JRE_HOME/lib
ENV JIRA_HOME /var/jira
VOLUME ["/opt/jira","/var/jira"]
EXPOSE 8080
CMD ["/opt/jira/bin/start-jira.sh"]
