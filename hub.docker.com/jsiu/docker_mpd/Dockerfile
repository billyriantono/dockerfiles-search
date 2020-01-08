# docker_mpd
FROM alpine:edge

LABEL version="0.21.14"
LABEL maintainers="[John Sing Dao Siu](https://github.com/J-Siu)"
LABEL name="docker_mpd"
LABEL usage="https://github.com/J-Siu/docker_mpd/blob/master/README.md"

COPY mpd.conf mpd.sh docker-compose.yml .env /
RUN chmod u+x /mpd.sh \
	&& mkdir /mpd \
	&& apk add --no-cache mpd==0.21.14-r0

EXPOSE 6600

CMD ["/mpd.sh"]