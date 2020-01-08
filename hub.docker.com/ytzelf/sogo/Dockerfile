FROM cschweingruber/sogo:latest

ENV CONFD_VERSION=0.16.0

# Install ssmtp
RUN apt-get update \
    && apt-get install -y ssmtp \
    && apt-get clean && rm -rf /var/lib/apt/lists/* /tmp/* /var/tmp/*

# Install CONFD
ADD https://github.com/kelseyhightower/confd/releases/download/v${CONFD_VERSION}/confd-${CONFD_VERSION}-linux-amd64 /usr/local/bin/confd
RUN chmod +x /usr/local/bin/confd
ADD confd /etc/confd
ADD confd.sh /etc/my_init.d/
RUN chmod +x /etc/my_init.d/confd.sh
