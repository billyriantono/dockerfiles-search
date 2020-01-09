FROM scaleway/java:armhf-latest

# Download
ADD http://dl.bintray.com/rundeck/rundeck-maven/rundeck-launcher-2.11.5.jar /opt/rundeck/
COPY content /

VOLUME ["/opt/rundeck/etc", \
        "/opt/rundeck/var", \
        "/opt/rundeck/projects", \
        "/opt/rundeck/server/config", \
        "/opt/rundeck/server/data", \
        "/opt/rundeck/server/logs"]

EXPOSE 4440 4443
ENTRYPOINT ["/opt/rundeck/entrypoint.sh"]
