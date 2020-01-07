FROM debian:buster

LABEL maintainer "miguelwill@gmail.com"

RUN apt-get update && \
    apt-get upgrade -y && \
    DEBIAN_FRONTEND=noninteractive apt-get install -y \
    x11vnc \
    xvfb \
    xterm \
    fluxbox \
    curl \
    firefox-esr && \
    apt-get clean

# Create and configure the VNC user
ARG VNCPASS
ENV VNCPASS ${VNCPASS:-secret}

RUN useradd remote --create-home --shell /bin/bash --user-group --groups adm,sudo && \
    echo "remote:$VNCPASS" | chpasswd

EXPOSE 80
EXPOSE 5900

VOLUME /data
WORKDIR /data

COPY main.sh /

ENTRYPOINT ["/main.sh"]
CMD ["default"]

