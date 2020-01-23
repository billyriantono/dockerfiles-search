FROM openjdk:8-jre-alpine
MAINTAINER Impact
LABEL application.component=impact-base

RUN echo "@testing http://nl.alpinelinux.org/alpine/edge/testing/" >> /etc/apk/repositories && \
    apk add --update --no-cache bash curl confd@testing py2-pip && \
    pip install awscli

WORKDIR /app

COPY entrypoint.sh /app/entrypoint.sh
RUN chmod +x /app/entrypoint.sh
ENTRYPOINT ["/app/entrypoint.sh"]
CMD ["java", "-jar", "/app/app.jar"]
