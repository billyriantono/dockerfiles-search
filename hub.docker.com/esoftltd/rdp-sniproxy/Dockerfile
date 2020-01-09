FROM alpine:3.8

RUN \
  apk --update --nocache add sniproxy && \
  rm -rf /var/cache/apk/*

COPY sniproxy.conf /etc/sniproxy.conf

EXPOSE 3389

CMD ["sniproxy", "-f"]
