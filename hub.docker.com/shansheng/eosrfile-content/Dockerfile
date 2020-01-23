FROM sergef/docker-library-alpine:edge

EXPOSE 6099 5900

ARG VNC_PASSWORD=changeme

RUN apk add --no-cache \
    openssh-server \
    x11vnc@testing \
    xvfb

ENV XVFB_WHD=1024x768x16

COPY entrypoint.sh /entrypoint.sh
RUN chmod +x /entrypoint.sh

# && x11vnc -storepasswd ${VNC_PASSWORD} \
ENTRYPOINT ["tini", "--", "/entrypoint.sh"]
