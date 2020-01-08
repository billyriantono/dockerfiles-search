FROM ubuntu:18.04
LABEL maintainer="Kirill_Shevchenko"
RUN apt-get update \
    && apt-get install -y tomcat9

# Prepare environment 
ENV CATALINA_HOME=/usr/share/tomcat9
ENV CATALINA_BASE=/var/lib/tomcat9
ENV CATALINA_TMPDIR=/CATALINA_TMPDIR
ENV JAVA_OPTS=-Djava.awt.headless=true

EXPOSE 8080
CMD ["/usr/share/tomcat9/bin/catalina.sh", "run"]


