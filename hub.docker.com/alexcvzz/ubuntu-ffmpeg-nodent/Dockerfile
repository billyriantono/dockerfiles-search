FROM ubuntu

LABEL maintainer="Alexandre Souza Aguiar <asouzaaguiar@gmail.com>"
LABEL description="gst-launch-1.0 is a tool that builds and runs basic GStreamer pipelines."

ENV ICECAST_HOST "127.0.0.1"
ENV ICECAST_PORT "8000"
ENV ICECAST_PASSWORD "hackme"
ENV ICECAST_MOUNT "stream.webm"

RUN apt-get -qq -y update && \
    apt-get -qq -y install ffmpeg && \
    apt-get clean

ADD start.sh /start.sh

CMD ["/start.sh"]
