FROM ruby:2.5

MAINTAINER Salvatore Ferrucci <salvatore@algonauti.com>

# Install.
RUN \
  apt-get update && \
  apt-get install -y build-essential curl git htop man unzip vim wget && \
  rm -rf /var/lib/apt/lists/*

# Installing Node.js via package manager
RUN \
  curl -sL https://deb.nodesource.com/setup_6.x | bash - && \
  apt-get install -y nodejs

# Install dumb-init (Very handy for easier signal handling of SIGINT/SIGTERM/SIGKILL etc.)
RUN wget https://github.com/Yelp/dumb-init/releases/download/v1.2.0/dumb-init_1.2.0_amd64.deb \
  && dpkg -i dumb-init_*.deb

COPY rootfs /

ENTRYPOINT ["dumb-init"]
