# ------------------------------------------------------------------------------
# Based on a work at https://github.com/docker/docker.
# ------------------------------------------------------------------------------
# Pull base image.
FROM kdelfour/supervisor-docker
MAINTAINER Kevin Delfour <kevin@delfour.eu>

# ------------------------------------------------------------------------------
# variables d'environnement
ENV USER lbf
ENV PASSWORD lsdm

# ------------------------------------------------------------------------------
# Install base
RUN apt-get update && apt-get install -y \
build-essential g++ curl libssl-dev apache2-utils git libxml2-dev sshfs imagemagick
RUN git config --global url."https://".insteadOf git://

# ------------------------------------------------------------------------------
# locales pour mongoDB
ENV LANG fr_FR.UTF-8

RUN locale-gen en_US && \
  locale-gen en_US.UTF-8 && \
  locale-gen fr_FR && \
  locale-gen fr_FR.UTF-8 && \
  dpkg-reconfigure locales

# ------------------------------------------------------------------------------
# Install Node.js
RUN curl -sL https://deb.nodesource.com/setup_6.x | sudo -E bash - \
  && apt-get install -y nodejs
#RUN curl -sL https://deb.nodesource.com/setup | sudo bash -\
#	&& apt-get install -y nodejs

#-------------------------------------------------------
# install graphCool
RUN npm install -g graphcool@next

# ------------------------------------------------------------------------------
# add user
RUN useradd -ms /bin/bash lbf && echo "lbf:lsdm38!" | chpasswd && adduser lbf sudo

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

# ------------------------------------------------------------------------------
# Clean up APT when done.
RUN apt-get clean && rm -rf /var/lib/apt/lists/* /tmp/* /var/tmp/*

# ------------------------------------------------------------------------------
# Expose ports.
EXPOSE 8080
EXPOSE 3000

ADD scripts/sed.sh /etc/scripts/
RUN chmod +x /etc/scripts/sed.sh
ENTRYPOINT ["/etc/scripts/sed.sh"]
# ------------------------------------------------------------------------------
# Start supervisor, define default command.
CMD ["supervisord", "-c", "/etc/supervisor/supervisord.conf"]
