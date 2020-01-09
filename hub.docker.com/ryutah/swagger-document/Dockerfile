FROM gradle:jdk8-alpine

USER root

WORKDIR /root

ARG SWAGGER_2_MARKUP_VERSION=1.3.3

RUN apk add --no-cache git

RUN git clone -b v${SWAGGER_2_MARKUP_VERSION} https://github.com/Swagger2Markup/swagger2markup-cli \
 && cd swagger2markup-cli \
 && gradle assemble \
 && mv build/libs/swagger2markup-cli-${SWAGGER_2_MARKUP_VERSION}.jar /usr/local/lib/ \
 && rm -rf /root/swagger2markup-cli \
 && rm -rf $HOME/.gradle

RUN apk add --no-cache ruby

RUN gem install --no-docu --no-ri asciidoctor

COPY ./convert.sh /root

ENTRYPOINT ["sh", "/root/convert.sh"]
