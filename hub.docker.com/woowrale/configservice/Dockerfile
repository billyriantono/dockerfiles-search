#=========================================
#Dockerfile
#=========================================
FROM woowrale/alpine-jdk8:latest
MAINTAINER woowrale@gmail.com
RUN apk --no-cache add netcat-openbsd
COPY configservice-0.0.2.jar /opt/lib/
COPY entrypoint.sh /opt/bin/
ENV TIME_WAITING="0s"
RUN chmod 755 /opt/bin/entrypoint.sh
CMD ["sh", "/opt/bin/entrypoint.sh"]
EXPOSE 8080
