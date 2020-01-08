FROM alpine:latest
MAINTAINER Tim Colbert <admin@tcolbert.net>

# Install nodejs and install tldr
RUN apk add --no-cache nodejs \
  && npm install -g --ignore-scripts tldr \
  && tldr --update

# If you building update this with configuration examples
# https://github.com/tldr-pages/tldr-node-client
COPY .tldrrc /root/.tldrrc

# Store the man pages for usage
VOLUME /root/.tldr

ENTRYPOINT [ "tldr" ]