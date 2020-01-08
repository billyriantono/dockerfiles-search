FROM java:8-jre

MAINTAINER MiYABiS

ENV DB_URL=
ENV DB_USER=
ENV DB_PASSWORD=

VOLUME /gitbucket
EXPOSE 8080 29418

ADD https://github.com/gitbucket/gitbucket/releases/download/4.26.0/gitbucket.war /opt/gitbucket.war

COPY entrypoint.sh /opt/entrypoint.sh
RUN ["chmod", "+x", "/opt/entrypoint.sh"]

CMD /opt/entrypoint.sh
