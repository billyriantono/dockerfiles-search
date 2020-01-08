FROM monokrome/node
MAINTAINER Brandon R. Stoner

RUN apt-get install -yy build-essential weechat curl

WORKDIR /tmp/docker-init
ADD ./src/ /tmp/docker-init/
RUN ./setup.sh

CMD ["/usr/local/bin/chat"]
