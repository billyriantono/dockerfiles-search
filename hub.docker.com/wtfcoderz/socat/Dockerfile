FROM alpine
RUN apk add --no-cache socat
ENV SOCKET /var/run/docker.sock
ENV PORT 2375
COPY docker-entrypoint.sh /
CMD ["/docker-entrypoint.sh"]
