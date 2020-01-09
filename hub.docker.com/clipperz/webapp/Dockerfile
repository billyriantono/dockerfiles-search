FROM tomcat:9.0-jdk11-adoptopenjdk-openj9

# remove all built-in examples
# and install fontconfig and ttf-dejavu for psi-probe
RUN rm -rf /usr/local/tomcat/webapps/* \
    && apt update  \
    && apt upgrade -y \
    && apt install -y fontconfig ttf-dejavu \
    && apt purge  -y \
    && rm -rf /var/lib/apt/lists

COPY files/entrypoint.sh /entrypoint.sh
COPY files/war/probe-3.3.1.war /probe.war
COPY files/lib/bcprov-jdk15on-164.jar /usr/local/tomcat/lib
COPY files/lib/opentracing-specialagent-1.5.0.jar /
COPY files/tomcat-users.xml /usr/local/tomcat/conf/

ENTRYPOINT ["/entrypoint.sh"]
EXPOSE 8080
CMD ["catalina.sh", "run"]
