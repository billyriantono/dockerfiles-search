FROM jeko/airbuild:19.0
RUN apt-get update && apt-get install -y xserver-xorg-video-dummy netcat-openbsd --no-install-recommends && rm -rf /var/lib/apt/lists/*
COPY docker-entry.sh /docker-entry.sh
COPY xorg.conf /xorg.conf
