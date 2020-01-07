FROM alpine:3.8

ENV TMPDIR /tmp
COPY entrypoint.sh /
RUN apk add --no-cache curl; rm -rf /var/cache/*; chmod +x /entrypoint.sh
ENTRYPOINT ["/entrypoint.sh"]
CMD ["curl"]
