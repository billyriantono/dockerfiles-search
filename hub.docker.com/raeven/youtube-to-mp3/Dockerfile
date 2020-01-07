FROM raeven/youtube-dl

MAINTAINER Emil Haugbergsmyr <emil@raeven.net>

VOLUME ["/download"]

ENTRYPOINT ["youtube-dl", "-o", "/download/%(title)s.%(ext)s", "--extract-audio", "--audio-format", "mp3"]

