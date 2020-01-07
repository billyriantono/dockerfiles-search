FROM debian:8.2

RUN ulimit -n 100 && apt-get update && apt-get install -y \
    apt-utils \
    make \
    build-essential \
    curl \
    wget \
    git \
    && curl -sL https://deb.nodesource.com/setup_0.12 | /bin/bash - && apt-get install -y \
    nodejs \
    && apt-get clean \
    && rm -rf /var/lib/apt/lists/* \
    && npm install -g gulp bower dtsm

CMD ["bin/bash"]
