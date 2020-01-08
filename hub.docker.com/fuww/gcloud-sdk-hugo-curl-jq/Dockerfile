FROM google/cloud-sdk:latest

RUN curl -sL https://deb.nodesource.com/setup_10.x | bash - && \
  apt-get install -y build-essential npm curl jq ca-certificates && \
  rm -rf /var/lib/apt/lists/*

RUN (cd /usr/local/bin; curl -qL https://github.com/gohugoio/hugo/releases/download/v0.54.0/hugo_extended_0.54.0_Linux-64bit.tar.gz | tar xz hugo)

ENV LANG=en_US.UTF-8
