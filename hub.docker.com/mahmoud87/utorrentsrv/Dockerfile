FROM debian:7
Maintainer Mahmoud Abdelrahman

# Create Utorrent user and group
#
RUN groupadd -r -g 766 utuser && \
    useradd -r -u 766 -g 766 -d /utorrentsrv -m utuser
    
#
# Add utorrent init script.
#
ADD utorrent.sh /utorrent.sh

RUN chown utuser: /utorrent.sh && \
    chmod 755 /utorrent.sh
  
#
# Install utorrent and all required dependencies.
#

RUN apt-get -q update \
    && apt-get install -qy curl libssl1.0.0 \
    && curl -s http://download.ap.bittorrent.com/track/beta/endpoint/utserver/os/linux-x64-debian-7-0 | tar xzf - --strip-components 1 -C utorrentsrv \
    && chown -R utuser:utuser /utorrentsrv \
    && apt-get -y remove curl \
    && apt-get -y autoremove \
    && apt-get -y clean \
    && rm -rf /var/lib/apt/lists/* \
    && rm -rf /tmp/*

#
# Define container settings.
#

VOLUME ["/config", "/downloads"]

EXPOSE 8080 6881

#
# Start utorrent.
#

WORKDIR /utorrentsrv

CMD ["/utorrent.sh"]
