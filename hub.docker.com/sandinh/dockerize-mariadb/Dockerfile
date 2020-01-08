FROM mariadb:10.1.14

RUN \
  apt-get update && \
  apt-get install -y --no-install-recommends wget && \
  wget https://github.com/jwilder/dockerize/releases/download/v0.2.0/dockerize-linux-amd64-v0.2.0.tar.gz && \
  tar -C /usr/local/bin -xzvf dockerize-linux-amd64-v0.2.0.tar.gz && \
  rm -f dockerize-linux-amd64-v0.2.0.tar.gz && \
  apt-get purge -y --auto-remove wget && \
  rm -rf /var/lib/apt/lists/*
