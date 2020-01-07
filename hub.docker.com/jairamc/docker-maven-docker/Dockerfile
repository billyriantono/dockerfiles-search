FROM maven:3-jdk-8

LABEL Maintainer="Jairam Chandar <jairam.chandar@meltwater.com>"

# Install docker
RUN apt-get update && \
    apt-get install -y --no-install-recommends \
        apt-transport-https \
        apt-utils \
        ca-certificates \
        software-properties-common \
        curl \
        ssh \
        git \
        sudo \
        jq && \
    # Install docker-ce binary
    curl -fsSL https://download.docker.com/linux/debian/gpg | sudo apt-key add - && \
    add-apt-repository "deb [arch=amd64] https://download.docker.com/linux/debian $(lsb_release -cs) stable" && \
    apt-get update && \
    apt-get install -y docker-ce && \
    # Cleanup
    apt-get autoclean && apt-get --purge -y autoremove && \
    rm -rf /var/lib/apt/lists/* /tmp/* /var/tmp/*