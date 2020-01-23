FROM gradle:jdk8 as builder

COPY --chown=gradle:gradle . /home/gradle/src
WORKDIR /home/gradle/src
RUN gradle build --no-daemon

FROM jetty:9.4.18-jre8
USER root
RUN mkdir -p /simplivity/var/private/config/current/ && chown -R jetty:jetty /simplivity/var/private/config/current/
RUN mkdir -p /simplivity/var/private/log/group/ && chown -R jetty:jetty /simplivity/var/private/log/group/
RUN mkdir -p /simplivity/var/private/temp/ && chown -R jetty:jetty /simplivity/var/private/temp/
COPY --from=builder /home/gradle/src/target/libs/docker-simplivity-plugin.war /var/lib/jetty/webapps/
EXPOSE 8080

