FROM alpine:3.6

RUN apk --no-cache add aria2 \
    && mkdir /data /aria2 \
    && touch /aria2/aria2.session

VOLUME ["/data"]

COPY aria2.conf /aria2/aria2.conf

EXPOSE 6800

CMD ["aria2c", "--conf-path=/aria2/aria2.conf"]
