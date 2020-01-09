FROM alpine:latest

MAINTAINER hyperchess

LABEL Remarks="Scalachess is a Chess API written in scala. Immutable and free of side effects. Check out more of ornicar's amazing work at https://github.com/ornicar"

#Install dependencies and set env vars
RUN apk update && \ 
    apk add --no-cache --virtual=.build-dependencies wget git curl && \
    apk add --no-cache ca-certificates bash openjdk8

ENV SCALA_VERSION=2.13.0 \
    SCALA_HOME=/opt/scala \
    SBT_VERSION=1.2.8 \
    SBT_HOME=/opt/sbt

#Install scala
RUN cd "/tmp" && \
    wget "https://downloads.lightbend.com/scala/${SCALA_VERSION}/scala-${SCALA_VERSION}.tgz" && \
    tar xzf "scala-${SCALA_VERSION}.tgz" && \
    mkdir "${SCALA_HOME}" && \
    rm "/tmp/scala-${SCALA_VERSION}/bin/"*.bat && \
    mv "/tmp/scala-${SCALA_VERSION}/bin" "/tmp/scala-${SCALA_VERSION}/lib" "${SCALA_HOME}" && \
    ln -s "${SCALA_HOME}/bin/"* "/usr/bin/" && \
    rm -rf "/tmp/"*
#Install sbt
RUN cd "/tmp" && \
    wget "https://piccolo.link/sbt-${SBT_VERSION}.tgz" && \
    tar -xvf "sbt-${SBT_VERSION}.tgz" && \
    mv "sbt" "${SBT_HOME}" && \
    ln -s "/${SBT_HOME}/bin/sbt" "/usr/bin" && \
    rm -rf "/tmp/"*
    
#Install, compile and test scalachess
RUN git clone git://github.com/ornicar/scalachess && \
    cd "scalachess" && \
    echo "Compiling" && \ 
    sbt compile && \
    echo "Running tests" && \
    sbt test

RUN apk del .build-dependencies

