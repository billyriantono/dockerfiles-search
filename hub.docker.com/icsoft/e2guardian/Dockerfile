# e2guardian Dockerfile to build container with latest e2guardian.
FROM icsoft/baseimage

# Update this for a different version of E2Guardian
ARG VERSION=5.3.2
# The listening port to expose
ARG LISTENPORT=8080

ENV PROXYIP 127.0.0.1
ENV PROXYPORT 3128

LABEL vendor="Icsoft Pty Ltd" \
    au.com.icsoft.version=${VERSION}

# Use baseimage-docker's init system.
CMD ["/sbin/my_init"]

# Install the essentials and dependancies for the build.
RUN apt-get update \
    && apt-get upgrade -y  -o Dpkg::Options::="--force-confold" \
    && apt-get install -y automake g++ zlib1g-dev pkg-config libpcre3-dev make \
    # Update this for newer versions, compile and install.
    && cd /tmp \
    && curl -k https://codeload.github.com/e2guardian/e2guardian/tar.gz/v${VERSION} > e2.tar.gz \
    && tar -zxvf e2.tar.gz \
    && cd /tmp/e2guardian-${VERSION} \
    && ./autogen.sh \
    && ./configure '--prefix=/usr' '--sysconfdir=/etc' '--localstatedir=/var' '--with-proxyuser=e2guardian' '--with-proxygroup=e2guardian' \
    && make \
    # Setup directory structure and install exe.
    && mkdir /etc/e2guardian \
    && cp src/e2guardian /usr/sbin/ \
    && mkdir /var/log/e2guardian \
    && mkdir /etc/service/e2guardian \
    # Add the e2guardian user
    && addgroup --system e2guardian \
    && adduser --no-create-home --home /nonexistent --ingroup e2guardian --system e2guardian \
    # Install supporting files 
    && mkdir -p /usr/share/e2guardian/languages \
    && cp -Rf data/languages /usr/share/e2guardian/ \
    && cp data/*.gif /usr/share/e2guardian/ \
    && cp data/*swf /usr/share/e2guardian/ \
    # Change ownership to e2guardian user
    && chmod 750 -Rf /usr/share/e2guardian \
    && chown -Rf e2guardian:e2guardian /usr/share/e2guardian /var/log/e2guardian \
    # Clean up
    && apt-get remove -y --purge curl libc6-dev libc-dev g++ make dpkg-dev autotools-dev libpcre3-dev zlib1g-dev \
    && find /usr/share/e2guardian -type f -name .in -delete \
    && apt-get clean \
    && apt-get autoremove -y \
    && rm -rf /var/lib/apt/lists/*

# Setup the service for baseimage-docker to run on start.
COPY e2guardian.sh /etc/service/e2guardian/run

# Enable access for configuration files and to view log files.
VOLUME /etc/e2guardian
VOLUME /var/log/e2guardian

# Listening port.
EXPOSE ${LISTENPORT}
