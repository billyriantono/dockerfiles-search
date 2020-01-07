FROM frolvlad/alpine-oraclejdk8:cleaned

ENV CATALINA_HOME /usr/local/tomcat
ENV PATH $CATALINA_HOME/bin:$PATH
RUN mkdir -p "$CATALINA_HOME"
WORKDIR $CATALINA_HOME


ENV TOMCAT_MAJOR 9
ENV TOMCAT_VERSION 9.0.2
ENV TOMCAT_SHA1 b59e1d658a4edbca7a81d12fd6f20203a4da9743

ENV TOMCAT_TGZ_URLS \
    # https://issues.apache.org/jira/browse/INFRA-8753?focusedCommentId=14735394#comment-14735394
    https://www.apache.org/dyn/closer.cgi?action=download&filename=tomcat/tomcat-$TOMCAT_MAJOR/v$TOMCAT_VERSION/bin/apache-tomcat-$TOMCAT_VERSION.tar.gz \
    # if the version is outdated, we might have to pull from the dist/archive :/
    https://www-us.apache.org/dist/tomcat/tomcat-$TOMCAT_MAJOR/v$TOMCAT_VERSION/bin/apache-tomcat-$TOMCAT_VERSION.tar.gz \
    https://www.apache.org/dist/tomcat/tomcat-$TOMCAT_MAJOR/v$TOMCAT_VERSION/bin/apache-tomcat-$TOMCAT_VERSION.tar.gz \
    https://archive.apache.org/dist/tomcat/tomcat-$TOMCAT_MAJOR/v$TOMCAT_VERSION/bin/apache-tomcat-$TOMCAT_VERSION.tar.gz


RUN set -eux; \
    \
    apk add --no-cache --virtual .fetch-deps \
    ca-certificates \
    openssl \
    ; \
    \
    success=; \
    for url in $TOMCAT_TGZ_URLS; do \
    if wget -O tomcat.tar.gz "$url"; then \
    success=1; \
    break; \
    fi; \
    done; \
    [ -n "$success" ]; \
    \
    echo "$TOMCAT_SHA1 *tomcat.tar.gz" | sha1sum -c -; \
    \
    success=; \
    tar -xvf tomcat.tar.gz --strip-components=1; \
    rm bin/*.bat; \
    rm tomcat.tar.gz*; 

EXPOSE 8080
CMD ["catalina.sh", "run"]