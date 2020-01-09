FROM debian:testing-slim

ADD https://github.com/Yelp/dumb-init/releases/download/v1.2.2/dumb-init_1.2.2_amd64 /usr/bin/dumb-init
RUN chmod +x /usr/bin/dumb-init
ENTRYPOINT ["/usr/bin/dumb-init", "--"]
CMD ["/bin/bash"]

RUN apt-get update \
 && apt-get upgrade -y \
 && apt-get install -y --no-install-recommends \
      g++ \
      libc6-dev \
      \
      g++-arm-linux-gnueabihf \
      libc6-dev-armhf-cross \
      \
      g++-aarch64-linux-gnu \
      libc6-dev-arm64-cross \
      \
      make \
      python3-pip \
      gnupg2 \
 && echo "deb https://download.docker.com/linux/debian stretch stable" > /etc/apt/sources.list.d/docker.list \
 && apt-key adv --fetch-keys https://download.docker.com/linux/debian/gpg \
 && apt-get update \
 && apt-get install -y --no-install-recommends \
      docker-ce \
      docker-ce-cli \
      containerd.io \
 && apt-get clean \
 && pip3 install --no-cache-dir --upgrade pip setuptools \
 && pip3 install --no-cache-dir cmake conan

ADD config.json /root/.docker/
