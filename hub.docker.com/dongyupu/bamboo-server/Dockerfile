FROM atlassian/bamboo-server:6.10.4

USER root

RUN sed '0,/JAVA_OPTS=\"/{s/JAVA_OPTS=\"/JAVA_OPTS=\"-javaagent:\/var\/atlassian\/application-data\/bamboo\/agent\/atlassian-agent.jar /}'< /opt/atlassian/bamboo/bin/setenv.sh > /opt/atlassian/bamboo/bin/setenv.sh
