FROM tomcat:8.5-jre8

USER root
RUN apt-get -yqq update && apt-get -yqq install curl zip && rm -rf /var/lib/apt/lists/*

user ${user}
COPY JAAS.config /usr/local/tomcat
COPY context.xml /usr/local/tomcat/conf
COPY web.xml /usr/local/tomcat/conf
ENV JAVA_OPTS="-Djava.security.auth.login.config="/usr/local/tomcat/JAAS.config" -Xmx1024m"
EXPOSE 8080:8080
