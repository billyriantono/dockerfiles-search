FROM node:5.9
MAINTAINER Niek Palm <dev.npalm@gmail.com>

ENV SWAGGER_UI_VERSION 2.1.4

WORKDIR /tmp

RUN curl -SL "https://github.com/swagger-api/swagger-ui/archive/v${SWAGGER_UI_VERSION}.tar.gz" | tar xz

RUN mv swagger-ui-${SWAGGER_UI_VERSION}/dist /swagger-ui && \
    rm -rf /tmp/swagger-ui-${SWAGGER_UI_VERSION} && \
    npm install http-server -g


WORKDIR /swagger-ui
EXPOSE 8080

ENTRYPOINT ["http-server", "/swagger-ui/", "-p 8080"]
CMD [""]
