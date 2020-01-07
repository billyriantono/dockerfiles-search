FROM yueyehua/debian-base
MAINTAINER Richard Delaplace "rdelaplace@yueyehua.net"
LABEL version="1.0.0"

ENV _PERL_VERSION=5.24.1

# Apt update and upgrade
RUN \
  apt-get -qq update && \
  apt-get -qq dist-upgrade -y;

# Install dependencies
RUN \
  apt-get -qq -y install gcc git-core build-essential libffi-dev libssl-dev \
    libcurl4-openssl-dev libreadline-dev;

# Clean all
RUN \
  apt-get -qq clean autoclean;

# Install plenv
RUN \
  git clone https://github.com/tokuhirom/plenv.git ~/.plenv && \
  git clone https://github.com/tokuhirom/Perl-Build.git \
    ~/.plenv/plugins/perl-build/;

# Install Perl
RUN \
  /root/.plenv/bin/plenv install ${_PERL_VERSION} && \
  /root/.plenv/bin/plenv global ${_PERL_VERSION};

# Install PerlCritic
RUN \
  echo 'yes' | cpan -i Perl::Critic;

# Export PATH
ENV PATH=$PATH:/root/.plenv/bin:/root/.plenv/shims

VOLUME ["/sys/fs/cgroup"]
CMD  ["/lib/systemd/systemd"]
