FROM alpine:3.9
LABEL maintainer="lyndon <snakeliwei@gmail.com>"

ENV MAILSLUPRPER_VERSION 1.14.1

RUN apk add --no-cache ca-certificates \
                       tzdata \
                       unzip \
                       curl \
    && mkdir -p /app \
    && curl -fSL https://github.com/mailslurper/mailslurper/releases/download/$MAILSLUPRPER_VERSION/mailslurper-$MAILSLUPRPER_VERSION-linux.zip -o /app/mailslurper.zip \
    && unzip /app/mailslurper.zip \
    && rm /app/mailslurper.zip \
    && cp /usr/share/zoneinfo/Asia/Shanghai /etc/localtime \
    && apk del unzip curl tzdata

WORKDIR /app
EXPOSE 8080 8085 2500

CMD ["./mailslurper"]
