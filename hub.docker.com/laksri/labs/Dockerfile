# ------------------------------------------------------------------------------
# Based on a work at https://github.com/docker/docker.
# ------------------------------------------------------------------------------
# Pull base image.
FROM kdelfour/supervisor-docker
MAINTAINER Kevin Delfour <kevin@delfour.eu>

# ------------------------------------------------------------------------------
# Install base
RUN apt-get update
RUN apt-get install -y build-essential g++ curl libssl-dev apache2-utils git libxml2-dev sshfs

# ------------------------------------------------------------------------------
# Install Node.js
RUN curl -sL https://deb.nodesource.com/setup_5.x | bash -
RUN apt-get install -y nodejs
    
# ------------------------------------------------------------------------------
# Install Cloud9
RUN git clone https://github.com/c9/core.git /cloud9
WORKDIR /cloud9
RUN scripts/install-sdk.sh

# Tweak standlone.js conf
RUN sed -i -e 's_127.0.0.1_0.0.0.0_g' /cloud9/configs/standalone.js 

# Add supervisord conf
ADD conf/cloud9.conf /etc/supervisor/conf.d/

# ------------------------------------------------------------------------------
# Add volumes
RUN mkdir /workspace
VOLUME /workspace

# **************************
#Install Java
RUN apt-get update \
    && apt-get -y install wget \
    && apt-get -y -f install default-jdk

# Install Go-lang 
RUN wget -O golang.tgz 'https://dl.google.com/go/go1.10.2.linux-amd64.tar.gz' \
    && tar -C /usr/local -xvzf golang.tgz \
    && rm golang.tgz 

ENV PATH="${PATH}:/usr/local/go/bin"

# install CF
RUN wget -O cf.tgz 'https://cli.run.pivotal.io/stable?release=linux64-binary&source=github' && \
    tar -C /usr/bin -xvzf cf.tgz && \
    rm cf.tgz

# install BX CF
RUN wget -O bxcf.tgz 'https://clis.ng.bluemix.net/download/bluemix-cli/0.6.7/linux64' && \
    tar -C /usr/local -xvzf bxcf.tgz && \
    rm bxcf.tgz && \
    /usr/local/Bluemix_CLI/install_bluemix_cli

# install git
RUN apt-get install --yes git
# **************************

# ------------------------------------------------------------------------------
# Clean up APT when done.
RUN apt-get clean && rm -rf /var/lib/apt/lists/* /tmp/* /var/tmp/*

# ------------------------------------------------------------------------------
# Expose ports.
EXPOSE 80
#EXPOSE 3000

# ------------------------------------------------------------------------------
# Start supervisor, define default command.
CMD ["supervisord", "-c", "/etc/supervisor/supervisord.conf"]
