# Base image
FROM scratch
MAINTAINER GetNinjas <tech@getninjas.com.br>

# Never prompt the user for choices on installation/configuration
ENV DEBIAN_FRONTEND noninteractive

# Set Bash as default process
CMD ["/bin/bash"]

# Add our squashed jessie
ADD debian-jessie.tar.bz2 /

# Install apt-fast by hand (ppas are working only for ubuntu distross)
RUN apt-get update && \
    apt-get -y install --no-install-recommends aria2 ca-certificates && \
    aria2c -x5 https://raw.githubusercontent.com/ilikenwf/apt-fast/master/apt-fast && \
    mv apt-fast /usr/bin && \
    chmod +x /usr/bin/apt-fast && \
    echo "MIRRORS=( 'http://httpredir.debian.org/debian' )" > /etc/apt-fast.conf && \
    rm -r /var/cache/apt/* /var/lib/apt/lists/*
