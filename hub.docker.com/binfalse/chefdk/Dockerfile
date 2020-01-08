FROM debian:testing-slim
MAINTAINER martin scharm <https://binfalse.de/contact>

# dependencies
RUN    apt-get update \
    && apt-get install --no-install-recommends -y \
            curl \
            vim \
            ca-certificates \
    && apt-get clean \
    && rm -rf /var/lib/apt/lists/*

# install chef dk
RUN curl https://omnitruck.chef.io/install.sh | bash -s -- -P chefdk -c stable -v 2.5.3

# default we
VOLUME /root/chef-repo
ENTRYPOINT /bin/bash
