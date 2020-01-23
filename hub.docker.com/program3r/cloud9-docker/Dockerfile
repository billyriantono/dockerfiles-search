FROM ubuntu

RUN apt-get update
RUN apt-get install -y python build-essential g++ curl libssl-dev apache2-utils git libxml2-dev sshfs

# ------------------------------------------------------------------------------
# Install Node.js
RUN curl -sL https://deb.nodesource.com/setup | bash -
RUN apt-get install -y nodejs

# ------------------------------------------------------------------------------
# Install Cloud9
RUN git clone https://github.com/c9/core.git /cloud9
WORKDIR /cloud9
RUN scripts/install-sdk.sh

# Tweak standlone.js conf
RUN sed -i -e 's_127.0.0.1_0.0.0.0_g' /cloud9/configs/standalone.js 

# ------------------------------------------------------------------------------
# Clean up APT when done.
RUN apt-get clean && rm -rf /var/lib/apt/lists/* /tmp/* /var/tmp/*

# ------------------------------------------------------------------------------
# Install forever
RUN npm install -g forever

# ------------------------------------------------------------------------------
# Add volumes
RUN mkdir /root/live
RUN mkdir /root/logs
RUN mkdir /root/logs/updates
RUN mkdir /root/app

VOLUME /root/live
VOLUME /root/logs
VOLUME /root/app

# ------------------------------------------------------------------------------
# Expose ports.
EXPOSE 80
EXPOSE 3000

# ------------------------------------------------------------------------------
# Add Proxy Support
ENV VIRTUAL_PORT 80
ENV VIRTUAL_EXPOSE 3000

ENTRYPOINT ["forever","--watch","--watchDirectory","/root/logs/updates","-v","--sourceDir","/cloud9","--spinSleepTime","3000","--workingDir","/cloud9","server.js","--listen","0.0.0.0","--port","80","-w", "/root/app"]