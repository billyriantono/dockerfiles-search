FROM node:10.4.0-alpine

# set timezone, add tini and add gitbook-cli
RUN apk add --update --no-cache tzdata tini && \
    cp /usr/share/zoneinfo/Asia/Tokyo /etc/localtime && \
    echo "Asia/Tokyo" > /etc/timezone && \
    apk del tzdata && \
    npm install -g gitbook-cli@2.3.2 && \
    gitbook install

EXPOSE 4000

EXPOSE 35729

WORKDIR /gitbook

ADD ./entrypoint.sh /entrypoint.sh

ENTRYPOINT ["/entrypoint.sh"]

CMD ["gitbook", "serve", "/gitbook", "/dist"]