FROM centos:7.6.1810
LABEL maintainer="vinu@xminds.com"
COPY ./setup.sh /tmp/setup.sh
RUN chmod +x /tmp/setup.sh && \
    /tmp/setup.sh && \
    rm -rf /tmp/setup.sh
ENV PATH=$PATH:/opt/flyway:/opt/tomcat/bin:/usr/share/phantomjs-2.1.1-linux-x86_64/bin
ENV JAVA_OPTS=-Duser.timezone=UTC
COPY ./entrypoint.sh /entrypoint.sh
RUN  chmod +x /entrypoint.sh
COPY ./ROOT /opt/tomcat/webapps/ROOT
ENTRYPOINT ["/entrypoint.sh"]