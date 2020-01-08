FROM accursoft/micro-debian:latest

MAINTAINER Yuki Hyou <snowleopard@amused.com.au>

ARG USER=windward
ARG GROUP=windward
ARG PUID=1000
ARG PGID=1000

ENV WINDWARD_SERVER_NAME="Windward Server" \
    WINDWARD_SERVER_WORLD="World" \
    WINDWARD_SERVER_PORT=5127 \
    WINDWARD_SERVER_PUBLIC=0

RUN apt-get update && apt-get install -y curl mono-complete && apt-get clean && rm -rf /var/lib/apt/lists && \
    mkdir -p /windward && \
    chmod ugo=rwx /windward && \
    addgroup --system --gid $PGID $GROUP && \
    adduser --system --uid $PUID --gid $PGID --shell /bin/sh --disabled-password $USER && \
    chown -R $USER:$GROUP /windward /home/windward && \
	ln -s /windward /home/windward/Windward
	
VOLUME /windward

EXPOSE $WINDWARD_SERVER_PORT

COPY ./windward.sh /

USER $USER

CMD ["/windward.sh"]
