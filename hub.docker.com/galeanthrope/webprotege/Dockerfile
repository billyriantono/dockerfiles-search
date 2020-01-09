FROM tomcat:8.5

ENV WEBPROTEGE_VERSION="3.0.0"
ENV JAVA_OPTS="$JAVA_OPTS -Dfile.encoding=UTF-8"

WORKDIR /usr/local/tomcat/webapps
RUN rm -rf * \
    && mkdir -p /data/webprotege \
    && wget -q -O webprotege.war https://github.com/Nyamiou/webprotege/releases/download/v${WEBPROTEGE_VERSION}-securemongo/webprotege-${WEBPROTEGE_VERSION}-securemongo.war \
    && unzip -q webprotege.war -d ROOT \
    && rm webprotege.war

RUN mkdir /etc/webprotege
COPY config/webprotege.properties /etc/webprotege/webprotege.properties
COPY config/mail.properties /etc/webprotege/mail.properties

RUN sed -i "s/\(application.version *= *\).*/\1$WEBPROTEGE_VERSION/" /etc/webprotege/webprotege.properties

EXPOSE 8080
VOLUME /data/webprotege

CMD ["catalina.sh", "run"]
