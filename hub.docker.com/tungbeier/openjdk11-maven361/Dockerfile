FROM alpine:3.9.4

LABEL name="tungbeier Maven 3.6.1 Image with openjdk 11" \
    maintainer="tung beier <beier.tung@web.de>" \
    summary="An alpine image to build a maven project with openjdk-11 and maven 3.6.1"

USER root

ENV TZ=Europe/Berlin
RUN ln -snf /usr/share/zoneinfo/$TZ /etc/localtime && echo $TZ > /etc/timezone

ARG MAVEN_VERSION=3.6.1
ARG MAVEN_CHECKSUM=b4880fb7a3d81edd190a029440cdf17f308621af68475a4fe976296e71ff4a4b546dd6d8a58aaafba334d309cc11e638c52808a4b0e818fc0fd544226d952544

RUN apk update --no-cache && \
    apk upgrade --no-cache && \
    apk add --no-cache curl && \
    apk --no-cache add openjdk11 --repository=http://dl-cdn.alpinelinux.org/alpine/edge/community && \
    curl https://archive.apache.org/dist/maven/maven-3/${MAVEN_VERSION}/binaries/apache-maven-${MAVEN_VERSION}-bin.tar.gz \
        --output /maven.tar.gz && \
    sha512sum maven.tar.gz | grep ${MAVEN_CHECKSUM} && \
    tar xzf maven.tar.gz && \
    mv apache-maven-${MAVEN_VERSION} /usr/share/maven && \
    ln -s /usr/share/maven/bin/mvn /usr/bin/mvn && \
    rm -f maven.tar.gz

ENV MAVEN_VERSION=${MAVEN_VERSION}
ENV M2_HOME /usr/share/maven
ENV M2 $M2_HOME/bin
ENV PATH $M2:$PATH

COPY ./entrypoint.sh /entrypoint.sh

RUN chmod +x /entrypoint.sh && \
    mkdir -vp /project && \
    mkdir -vp /repository && \ 
    adduser -D -H -G wheel -s sh developer && \
    chown -R developer:wheel /project && \
    chown -R developer:wheel /repository

COPY ./settings.xml /usr/share/maven/conf/settings.xml

USER developer

WORKDIR /project
VOLUME ["/project", "/repository"]

ENTRYPOINT [ "/entrypoint.sh" ]
CMD ["mvn", "verify"]
