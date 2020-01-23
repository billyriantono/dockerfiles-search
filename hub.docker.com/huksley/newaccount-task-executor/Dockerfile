FROM tomcat:8-jre8
RUN apt update
RUN apt install -y curl
RUN curl -o /task-executor.war https://github.com/huksley/newaccount/releases/download/latest/task-executor.war -k -L -H "User-Agent: Docker-download-release-by-github-huksley"
RUN mv /task-executor.war /usr/local/tomcat/webapps/


