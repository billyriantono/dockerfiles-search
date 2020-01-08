FROM openjdk:8-jre-alpine

LABEL maintainer="190ikp <ikp190[at]outlook.com>"

ENV GITBUCKET_VER=4.31.1
ENV GITBUCKET_EXTRA_DEPS="git procps"

ADD https://github.com/gitbucket/gitbucket/releases/download/$GITBUCKET_VER/gitbucket.war /opt/gitbucket.war

COPY gitbucket.sh /opt/gitbucket.sh

RUN ln -s /gitbucket /root/.gitbucket \
    && chmod +x /opt/gitbucket.sh

VOLUME /gitbucket

EXPOSE 8080
EXPOSE 29418

CMD '/opt/gitbucket.sh'