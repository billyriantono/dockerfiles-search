FROM ubuntu

LABEL maintainer="Alexandre Souza Aguiar <asouzaaguiar@gmail.com>"
LABEL description="gst-launch-1.0 is a tool that builds and runs basic GStreamer pipelines."

ENV VIDEOTESTSRC "is-live=true"
ENV THEORAENC "quality=40"
ENV AUDIOTESTSRC "volume=0.1 wave=ticks is-live=true"
ENV VORBISENC "quality=0.1"
ENV OGGMUX "max-delay=100000000 max-page-delay=100000000 name=mux"
ENV SHOUT2SEND_HOST "127.0.0.1"
ENV SHOUT2SEND_PORT "8000"
ENV SHOUT2SEND_PASSWORD "hackme"
ENV SHOUT2SEND_MOUNT "stream.ogv"

RUN apt-get -qq -y update && \
    apt-get -qq -y install libgstreamer1.0-0 gstreamer1.0-plugins-base gstreamer1.0-plugins-good gstreamer1.0-plugins-bad gstreamer1.0-plugins-ugly gstreamer1.0-libav gstreamer1.0-doc gstreamer1.0-tools && \
    apt-get clean

ADD start.sh /start.sh

CMD ["/start.sh"]
