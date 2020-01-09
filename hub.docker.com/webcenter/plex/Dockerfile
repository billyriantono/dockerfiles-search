FROM plexinc/pms-docker:latest
MAINTAINER Sebastien LANGOUREAUX <linuxworkgroup@hotmail.com>


# Add libs & tools
RUN apt-get update && \
    apt-get install -y --no-install-recommends libfuse-dev autoconf automake wget build-essential git  && \
    apt-get clean && \
    rm -rf /var/lib/apt/lists/*

# Install rar2fs
COPY assets/install_rar2fs.sh /tmp/
RUN /bin/sh /tmp/install_rar2fs.sh
RUN mkdir /data_unrar


# CLEAN Image
RUN apt-get remove -y autoconf build-essential git automake && \
    apt autoremove -y
RUN rm -rf /tmp/* /var/tmp/*

# Add start script
COPY start_rar2fs.sh /etc/cont-init.d/00-start_rar2fs.sh

