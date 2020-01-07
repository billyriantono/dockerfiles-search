FROM smebberson/alpine-nodejs

ENV MAVEN_VERSION_MAJOR 3
ENV MAVEN_VERSION 3.3.9

RUN mkdir /opt && \
        cd /opt && \
        apk -Uuv add groff less python py-pip openjdk8 curl git && \
        curl -jksSL http://apache.mindstudios.com/maven/maven-${MAVEN_VERSION_MAJOR}/${MAVEN_VERSION}/binaries/apache-maven-${MAVEN_VERSION}-bin.tar.gz \
        | tar -xzf - -C /opt &&\
        ln -s /opt/apache-maven-${MAVEN_VERSION} /opt/apache-maven &&\
        mkdir -p /aws && \
        pip install awscli && \
        rm /var/cache/apk/*

ENV JAVA_HOME /usr/lib/jvm/default-jvm
ENV PATH ${PATH}:/opt/apache-maven/bin:/aws:/opt/node_modules/.bin/

