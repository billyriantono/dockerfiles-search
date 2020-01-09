FROM alpine
RUN apk --no-cache add squid

ENTRYPOINT ["/usr/sbin/squid"]
CMD ["--foreground"]

EXPOSE 443/tcp
