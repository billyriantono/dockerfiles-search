FROM debian

LABEL version="1.0" 
LABEL maintainer="Kaspar Pflugshaupt <kpflugshaupt@gmail.com>"

COPY entrypoint.sh /
RUN apt-get update && apt-get install -y cowsay fortune && chmod +x /entrypoint.sh

ENTRYPOINT ["/entrypoint.sh"]
