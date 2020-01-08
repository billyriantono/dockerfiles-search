FROM pataquets/unoconv

RUN \
  apt-get update && \
  DEBIAN_FRONTEND=noninteractive \
    apt-get install -y \
      xvfb \
  && \
  apt-get clean && \
  rm -rf /var/lib/apt/lists/

ENTRYPOINT [ "xvfb-run", "/usr/bin/unoconv", "--server=0.0.0.0", "--port=2002", "--verbose" ]
