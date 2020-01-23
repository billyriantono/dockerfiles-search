FROM openjdk:8u181-alpine3.8
LABEL maintainer="szyn <aqr.aqua@gmail.com>"

ENV EMBULK_VERSION 0.9.7
ENV EMBULK_HOME /home/embulk
ENV EMBULK_BIN ${EMBULK_HOME}/.embulk/bin/embulk
ENV PATH=${EMBULK_HOME}/.embulk/bin:${PATH}

RUN apk add --no-cache jruby curl && \
    adduser -D embulk && \
    curl --create-dirs -o ${EMBULK_BIN} \
         -L "https://dl.bintray.com/embulk/maven/embulk-${EMBULK_VERSION}.jar" && \
    chown -R embulk:embulk ${EMBULK_HOME} && \
    chmod +x ${EMBULK_BIN} && \
    apk del --purge curl

USER embulk
WORKDIR ${EMBULK_HOME}

RUN embulk gem install embulk-input-mysql \
                       embulk-input-postgresql \
                       embulk-input-s3 \
                       embulk-filter-add_time \
                       embulk-output-s3 \
                       embulk-output-td

ENTRYPOINT [ "java", "-jar", "/home/embulk/.embulk/bin/embulk" ]
