FROM ubuntu:14.04
MAINTAINER Filip Wieladek <filip@beekeeper.io>

LABEL Description="This is a simple image containing just Git." \
      Vender="Beekeeper" \
      Version="0.1"

RUN apt-get update && \
    apt-get -q -y install git && \
    apt-get clean && \
    rm -rf /var/lib/apt/lists/* /tmp/* /var/tmp/*


WORKDIR /opt/git
VOLUME ["/opt/git"]
ENTRYPOINT ["git"]
