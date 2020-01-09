FROM node:lts-slim

ENV NPM_CONFIG_LOGLEVEL info

RUN apt-get update -y && \
    apt-get install -qqy --no-install-recommends && \
    apt-get install -y ssh rsync openssh-client git && \
    rm -rf /var/lib/apt/lists/* /tmp/* /var/tmp/*

# RUN ln -s /bin/bash /usr/local/bin/bash

# CMD ["/bin/bash"]
