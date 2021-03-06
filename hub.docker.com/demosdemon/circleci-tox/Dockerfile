FROM demosdemon/tox-base

LABEL maintainer="Brandon LeBlanc <brandon@leblanc.codes>"

# make Apt non-interactive
RUN set -eux; \
    echo 'APT::Get::Assume-Yes "true";' > /etc/apt/apt.conf.d/90circleci; \
    echo 'DPkg::Options "--force-confnew";' >> /etc/apt/apt.conf.d/90circleci;

# man directory is missing in some base images
# https://bugs.debian.org/cgi-bin/bugreport.cgi?bug=863199
RUN set -eux; \
    apt-get update && \
    mkdir -p /usr/share/man/man1 && \
    apt-get install --no-install-recommends -y \
        apt \
        bzip2 \
        ca-certificates \
        curl \
        git \
        gnupg \
        gzip \
        locales \
        net-tools \
        netcat \
        openssh-client \
        parallel \
        sudo \
        tar \
        unzip \
        wget \
        xvfb \
        zip \
    ; \
    apt-get clean; rm -rf /var/lib/apt/lists/* /tmp/* /var/tmp/*;

# Set timezone to Central by default
RUN ln -sf /usr/share/zoneinfo/America/Chicago /etc/localtime

# install jq
RUN set -eux; \
    JQ_URL="https://circle-downloads.s3.amazonaws.com/circleci-images/cache/linux-amd64/jq-latest"; \
    curl --silent --show-error --location --fail --retry 3 --output /usr/bin/jq $JQ_URL; \
    chmod +x /usr/bin/jq; \
    jq --version;

# Install Docker

# Docker.com returns the URL of the latest binary when you hit a directory listing
# We curl this URL and `grep` the version out.
# The output looks like this:

#>    # To install, run the following commands as root:
#>    curl -fsSLO https://download.docker.com/linux/static/stable/x86_64/docker-17.05.0-ce.tgz && tar --strip-components=1 -xvzf docker-17.05.0-ce.tgz -C /usr/local/bin
#>
#>    # Then start docker in daemon mode:
#>    /usr/local/bin/dockerd

RUN set -eux; \
    export DOCKER_VERSION=$(curl --silent --fail --retry 3 https://download.docker.com/linux/static/stable/x86_64/ | grep -o -e 'docker-[.0-9]*\.tgz' | sort -r | head -n 1); \
    DOCKER_URL="https://download.docker.com/linux/static/stable/x86_64/${DOCKER_VERSION}"; \
    echo Docker URL: $DOCKER_URL; \
    curl --silent --show-error --location --fail --retry 3 --output /tmp/docker.tgz "${DOCKER_URL}"; \
    ls -lha /tmp/docker.tgz; tar -xz -C /tmp -f /tmp/docker.tgz; \
    mv /tmp/docker/* /usr/bin; \
    rm -rf /tmp/docker /tmp/docker.tgz; \
    which docker; \
    (docker version || true);

# docker compose
RUN set -eux; \
    COMPOSE_URL="https://circle-downloads.s3.amazonaws.com/circleci-images/cache/linux-amd64/docker-compose-latest"; \
    curl --silent --show-error --location --fail --retry 3 --output /usr/bin/docker-compose $COMPOSE_URL; \
    chmod +x /usr/bin/docker-compose; \
    docker-compose version;

# install dockerize
RUN set -eux; \
    DOCKERIZE_URL="https://circle-downloads.s3.amazonaws.com/circleci-images/cache/linux-amd64/dockerize-latest.tar.gz"; \
    curl --silent --show-error --location --fail --retry 3 --output /tmp/dockerize-linux-amd64.tar.gz $DOCKERIZE_URL; \
    tar -C /usr/local/bin -xzvf /tmp/dockerize-linux-amd64.tar.gz; \
    rm -rf /tmp/dockerize-linux-amd64.tar.gz; \
    dockerize --version;

RUN set -eux; \
    groupadd --gid 3434 circleci; \
    useradd --uid 3434 --gid circleci --shell /bin/bash --create-home circleci; \
    echo 'circleci ALL=NOPASSWD: ALL' >> /etc/sudoers.d/50-circleci; \
    echo 'Defaults    env_keep += "DEBIAN_FRONTEND"' >> /etc/sudoers.d/env_keep;

# Install pipenv and poetry
RUN pip install pipenv poetry

USER circleci

CMD ["/bin/sh"]
