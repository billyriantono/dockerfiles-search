FROM linuxserver/sabnzbd:latest

RUN \
  apt-get update && \
  apt-get install -y \
  git \
  python-pip

RUN \
  pip install --upgrade pip && \
  hash -r pip && \
  pip install requests
