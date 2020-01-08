FROM debian

RUN set -ex \
  && apt-get update \
  && apt-get install -y \
    curl \
    dnsutils \
    fish \
    git \
    htop \
    locales \
    man \
    netcat \
    python3 \
    python3-pip \
    tcpdump \
    traceroute \
    unzip \
    vim \
    wget \
    whois \
  && localedef -i en_US -c -f UTF-8 -A /usr/share/locale/locale.alias en_US.UTF-8 \
  && /usr/bin/fish -c fish_update_completions

ENV LANG en_US.utf8
CMD /usr/bin/fish
