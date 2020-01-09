FROM maciver40/ubuntu-base
LABEL maintainer="robert@eisenmann.email"

VOLUME [ "/video" ]
VOLUME [ "/export" ]

RUN \
    apt-get update && \
    apt-get install -y \
           libavcodec-extra \
           ffmpeg \
           handbrake-cli \
           mkvtoolnix \
           ruby \
           mediainfo \
           npm \
           python \
           python-setuptools \
           python3 \
           python3-setuptools \           
           python-pip && \
    gem install video_transcoding && \
    npm i batch-transcode-video -g && \
    mkdir /automp4 && cd /automp4 && \
    git clone https://github.com/mdhiggins/sickbeard_mp4_automator.git . && \
    pip install \
           requests \
           requests[security] \
           requests-cache \
           babelfish \
           tmdbsimple \
           tvnamer \
           qtfaststart \
           "guessit<2" \
           "subliminal<2" && \
    pip uninstall --yes stevedore && yes | pip install "stevedore==1.19.1"
