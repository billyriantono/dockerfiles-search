FROM sillelien/base-java
MAINTAINER Patrick Grimard <pgrimard@gmail.com>
ADD response.varfile /opt/response.varfile
RUN apk add --update curl tar gzip bash && \
  cd /opt && \
  curl -O http://cdn.mysql.com//Downloads/Connector-J/mysql-connector-java-5.1.38.tar.gz && \
  tar xvfz mysql-connector-java-5.1.38.tar.gz && \
  curl https://downloads.atlassian.com/software/jira/downloads/atlassian-servicedesk-3.1.2-jira-7.1.2-x64.bin -o jira.bin && \
  chmod +x jira.bin && \
  ./jira.bin -q -varfile response.varfile && \
  cp mysql-connector-java-5.1.38/mysql-connector-java-5.1.38-bin.jar atlassian/jira/lib/
ENTRYPOINT ["/opt/atlassian/jira/bin/catalina.sh", "run"]
