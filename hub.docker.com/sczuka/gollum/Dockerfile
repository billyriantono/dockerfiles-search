FROM debian

LABEL maintainer="Armin Sczuka <sczuka@hotmail.com>"

RUN apt-get update && \
  apt-get upgrade -y && \
  apt-get install -y -q \
    build-essential ruby \
    python \ 
    python-docutils \
    ruby-bundler \
    ruby-dev \
    libicu-dev \
    libreadline-dev \
    libssl-dev \
    zlib1g-dev \
    git-core && \
apt-get clean

RUN gem install \
  gollum \
  redcarpet \
  github-markdown \
  asciidoctor \
  asciidoctor-diagram \
  coderay

RUN mkdir /root/wikidata
RUN git init /root/wikidata

# Expose default gollum port 4567
EXPOSE 4567

ENTRYPOINT ["/usr/local/bin/gollum", "/root/wikidata"]
