FROM ubuntu:16.04

LABEL maintainer="efec/git Docker Maintainers <li.jun.kuma@gmail.com>"

# Install ssh, git, node
RUN echo 'debconf debconf/frontend select Noninteractive' | debconf-set-selections && \
    apt-get update && apt-get install --no-install-recommends --no-install-suggests -y apt-utils && \
    apt-get install --no-install-recommends --no-install-suggests -y libssl-dev openssl ca-certificates openssh-server wget git && \
    apt-get clean && rm -rf /var/lib/apt/lists/* /tmp/* /var/tmp/*

VOLUME ['/root/.ssh']

# Define default command.
CMD ["/bin/bash"]