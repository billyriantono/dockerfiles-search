FROM openjdk:8u131-jre-alpine

ADD https://github.com/litaiqing/docker-build/releases/download/v1.0/yanagishima-20.0.zip /yanagishima.zip

RUN unzip /yanagishima.zip -d / && \
    chmod u+x /yanagishima-20.0/bin/yanagishima*

WORKDIR /yanagishima-20.0/

EXPOSE 8080

CMD ["bash", "bin/yanagishima-start.sh"]