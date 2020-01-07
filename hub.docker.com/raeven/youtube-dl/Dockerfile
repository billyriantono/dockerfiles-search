FROM ubuntu:12.04

MAINTAINER Emil Haugbergsmyr <emil@raeven.net>

RUN apt-get update && apt-get upgrade -y && apt-get install -y python-setuptools ffmpeg libavcodec-extra-53

RUN easy_install -U youtube-dl

VOLUME ["/download"]

ENTRYPOINT ["youtube-dl", "-o", "/download/%(title)s.%(ext)s"]

