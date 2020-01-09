FROM python:2

RUN \
  apt-get update && \
  DEBIAN_FRONTEND=noninteractive \
    apt-get -y install \
      python-gtk2 \
      python-xlib \
  && \
  apt-get clean && \
  rm -rf /var/lib/apt/lists/ \
  && \
  pip install --no-cache-dir key-mon

ENTRYPOINT [ "key-mon" ]
