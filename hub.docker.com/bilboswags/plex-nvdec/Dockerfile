FROM linuxserver/plex

ADD ./plex-nvdec-patch.sh /tmp/plex-nvdec-patch.sh

RUN \
  chmod +x /tmp/plex-nvdec-patch.sh && \
  bash -c /tmp/plex-nvdec-patch.sh && \
  rm /tmp/plex-nvdec-patch.sh
