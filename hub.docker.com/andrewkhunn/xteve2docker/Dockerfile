FROM alpine:latest
LABEL maintainer="andrewkhunn"

RUN apk update && apk upgrade && apk add --no-cache ca-certificates curl ffmpeg tzdata vlc && \
    addgroup -S xteve && adduser -S xteve -G xteve && \
    mkdir /tmp/xteve && chown xteve:xteve /tmp/xteve && \
    mkdir -p /xteve
ADD https://raw.githubusercontent.com/xteve-project/xTeVe-Downloads/master/xteve_linux_amd64.zip /tmp/xteve_linux_amd64.zip
RUN unzip -o /tmp/xteve_linux_amd64.zip -d /xteve && \
    rm /tmp/xteve_linux_amd64.zip && \
    chmod +x /xteve/xteve

ENV TZ=America/New_York
RUN ln -snf /usr/share/zoneinfo/$TZ /etc/localtime && echo $TZ > /etc/timezone && \
    sed -i 's/geteuid/getppid/' /usr/bin/vlc

USER xteve
RUN mkdir /home/xteve/.xteve && \
    mkdir /home/xteve/.xteve/backup

VOLUME /home/xteve/.xteve

EXPOSE 34400

ENTRYPOINT ["/xteve/xteve"]
CMD ["-port=34400", "-branch=beta"]

HEALTHCHECK --interval=1m --retries=3 --start-period=1m --timeout=5s \
  CMD curl -f http://localhost:34400/web/ || exit 1
