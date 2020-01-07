FROM python:3-alpine
LABEL maintainer "Aurélien JANVIER <dev@ajanvier.fr>"

# Install useful packages
RUN apk --no-cache add wget unzip

# Install application dependencies
RUN pip install pafy \
    feedparser \
    toml \
    requests-toolbelt \
    youtube_dl

# Download application
RUN wget https://github.com/mister-monster/YouTube2PeerTube/archive/master.zip && \
    unzip master.zip -d / && \
    rm master.zip && \
    mv /YouTube2PeerTube-master /app

WORKDIR /app

# Copying config
COPY example_config.toml /app/config.toml

# Copying the run script
COPY run.sh /run.sh
RUN chmod u+rwx /run.sh

# Default environment variables
ENV VIDEO_DOWNLOAD_DIR=/videos/ \
    USE_PT_HTTP_IMPORT=false \
    DELETE_VIDEOS=false \
    POLL_FREQUENCY=180 \
    PEERTUBE_CHANNEL_CATEGORY=10 \
    PEERTUBE_CHANNEL_DEFAULT_LANG=en \
    PEERTUBE_CHANNEL_NSFW=false \
    PEERTUBE_CHANNEL_COMMENTS_ENABLED=true \
    PEERTUBE_CHANNEL_PRIVACY=1 \
    PEERTUBE_VIDEO_PREFERRED_EXTENSION=mp4 \
    PEERTUBE_VIDEO_MAX_RESOLUTION=1080

# Removing useless packages
RUN apk del wget unzip

ENTRYPOINT [ "/run.sh" ]
