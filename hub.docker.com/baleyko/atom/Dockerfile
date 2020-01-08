FROM ubuntu:bionic

ENV ATOM_VERSION 1.42.0
ENV DISPLAY :1

LABEL maintainer="Valery Baleyko <baleyko@gmail.com>"
LABEL version="${ATOM_VERSION}"
LABEL description="Atom text editor"

WORKDIR /

RUN apt-get update -yqq && \
  apt-get install -y --no-install-recommends \
    ca-certificates \
    curl \
    git \
    libgconf-2-4 \
    libgtk-3-0 \
    libxtst6 \
    libxss1 \
    libasound2 \
    xdg-utils \
    libnotify4 \
    libnss3 \
    gvfs-bin \
    policykit-1 \
    python \
    xvfb && \
  curl -L https://github.com/atom/atom/releases/download/v${ATOM_VERSION}/atom-amd64.deb > /tmp/atom.deb && \
  dpkg -i /tmp/atom.deb && \
  apt-get purge -y \
    ca-certificates \
    curl && \
  rm -f /tmp/atom.deb && \
  apt-get -y autoremove && \
  apt-get clean && \
  rm -rf /var/lib/apt/lists/*

ADD . .

ENTRYPOINT ["docker-entrypoint.sh"]
