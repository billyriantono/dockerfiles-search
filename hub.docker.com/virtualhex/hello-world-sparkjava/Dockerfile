FROM openjdk:8-jre-alpine
LABEL maintainer="Daniel Anderson \"daniel@virtual-hex.com\""
ADD web-server /web-server
ADD app-lib/web-server-1.0.0-RC-SNAPSHOT.jar /web-server/lib/web-server-1.0.0-RC-SNAPSHOT.jar
RUN ["chmod", "+x", "/web-server/bin/web-server"]
ENTRYPOINT ["/web-server/bin/web-server"]
