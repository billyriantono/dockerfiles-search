FROM lsiobase/ubuntu:xenial

RUN \
  # Install dependencies
  apt-get update && \
  apt-get full-upgrade -y && \
  apt-get install --no-install-recommends -y \
    git \
    python \
    python-pip \
    python-dev \
    g++ \
    apt-transport-https \
    ca-certificates \
    curl \
    gnupg2 \
    software-properties-common \
    unzip \
    man-db && \
  # Add docker repo key to apt
  curl -fsSL https://download.docker.com/linux/ubuntu/gpg | apt-key add - && \
  # Add docker repo
  add-apt-repository "deb [arch=amd64] https://download.docker.com/linux/ubuntu $(lsb_release -cs) stable" && \
  # Update
  apt-get update && \
  # Install docker client tools
  apt-get install --no-install-recommends -y docker-ce-cli && \
  # Get plex_autoscan
  git clone --depth 1 --single-branch https://github.com/axc97c/plex_autoscan.git /plex_autoscan && \
  # Setup service file
  cp /plex_autoscan/system/plex_autoscan.service /etc/systemd/system/plex_autoscan.service && \
  # Install/update pip and requirements
  pip install --no-cache-dir --upgrade pip setuptools wheel && \
  # PIP upgrade bug https://github.com/pypa/pip/issues/5221
  hash -r pip && \
  pip install -r /plex_autoscan/requirements.txt && \
  # Install rclone to decrpyt stuff
  curl https://rclone.org/install.sh | bash && \
  # Remove dependencies
  apt-get purge -y --auto-remove \
    python-dev \
    g++ && \
  # Clean apt cache
  apt-get clean all && \
  rm -rf \
    /tmp/* \
    /var/lib/apt/lists/* \
    /var/tmp/*

ENV \
  # Plex_autoscan config file
  PLEX_AUTOSCAN_CONFIG=/config/config.json \
  # Plex_autoscan queue db file
  PLEX_AUTOSCAN_QUEUEFILE=/config/queue.db \
  # Plex_autoscan log file
  PLEX_AUTOSCAN_LOGFILE=/config/plex_autoscan.log \
  # Plex_tokenfile google drive token
  PLEX_AUTOSCAN_TOKENFILE=/config/token.json \
  # Plex_autoscan enable docker and disable sudo
  USE_DOCKER=true \
  USE_SUDO=false

EXPOSE 3467

ENTRYPOINT ["python", "plex_autoscan/scan.py", "server"]