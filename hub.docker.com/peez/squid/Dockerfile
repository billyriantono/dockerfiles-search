FROM alpine:latest
RUN apk add --no-cache squid
ENV SQUID_ARGS " "
EXPOSE 3128
CMD ["sh", "-c", "/usr/sbin/squid -N ${SQUID_ARGS}"]