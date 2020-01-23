FROM nextcloud:latest

RUN a2enmod headers

RUN apt-get update && apt-get install -y \
        ffmpeg \
        fonts-noto-cjk \
        fonts-noto-mono \
        fonts-noto-hinted && \
    rm -rf /var/lib/apt/lists/*

RUN mkdir /mnt/cloudfuse

VOLUME /mnt/cloudfuse