FROM node:10.15.3

# Apt-get install should not cache
COPY 02nocache /etc/apt/apt.conf.d/02nocache

# Hopefully, there will be no cache...
COPY 01_nodoc /etc/dpkg/dpkg.cfg.d/01_nodoc

RUN build_deps="python-dev python-setuptools libpython-dev" && \
    apt-get update && \
    DEBIAN_FRONTEND=noninteractive apt-get install -y --no-install-recommends ${build_deps} && \
    curl -s https://packagecloud.io/install/repositories/github/git-lfs/script.deb.sh | bash && \
    DEBIAN_FRONTEND=noninteractive apt-get install -y --no-install-recommends git-lfs python-pip jq \
    zip sudo vim && \
    git lfs install && \
    pip install awscli && \
    DEBIAN_FRONTEND=noninteractive apt-get purge -y --auto-remove ${build_deps} && \
    rm -r /var/lib/apt/lists/* && \
    # allow the node user use sudo without a password
    echo "node ALL=(ALL) NOPASSWD: ALL" >> /etc/sudoers

COPY entrypoint.sh /home/node/entrypoint.sh
RUN chown node:node /home/node/entrypoint.sh

# default user to run commands on the container, also all RUN commands from this point are executed
# with this user
USER node

WORKDIR /home/node

RUN chmod +x /home/node/entrypoint.sh

CMD ["./entrypoint.sh"]
