FROM fktym/alpine-sdkman:alpine3.9 AS builder

ENV JAVA_VERSION=11.0.3-amzn
ENV JAVA_HOME=/root/.sdkman/candidates/java/$JAVA_VERSION
ENV MAVEN_VERSION=3.6.0
ENV MAVEN_HOME=/root/.sdkman/candidates/maven/$MAVEN_VERSION

SHELL ["/bin/bash", "-c"]
RUN . ~/.sdkman/bin/sdkman-init.sh && \
    sdk update && \
    sdk install java $JAVA_VERSION && \
    sdk install maven $MAVEN_VERSION && \
    sdk flush broadcast && \
    sdk flush archives && \
    sdk flush temp && \
    find $JAVA_HOME -name "*src.zip" -exec rm {} \; && \
    : "install python/pip" && \
    apk update && \
    apk upgrade && \
    apk add --no-cache python3 && \
    python3 -m ensurepip && \
    rm -r /usr/lib/python*/ensurepip && \
    pip3 install --upgrade pip setuptools && \
    if [ ! -e /usr/bin/pip ]; then ln -s pip3 /usr/bin/pip ; fi && \
    if [[ ! -e /usr/bin/python ]]; then ln -sf /usr/bin/python3 /usr/bin/python; fi && \
    : "install aws cli" && \
    pip install --upgrade awscli awsebcli && \
    : "install docker" && \
    apk add --no-cache docker && \
    : "install git" && \
    apk add --no-cache git && \
    : "require build tools" && \
    apk add --no-cache perl-utils && \
    rm -r /root/.cache    

ENV PATH="$PATH:$JAVA_HOME/bin:$MAVEN_HOME/bin"

