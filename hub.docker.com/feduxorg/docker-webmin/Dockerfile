FROM perl:5

ENV DEBIAN_FRONTEND=noninteractive
ENV WEBMIN_VERSION 860

WORKDIR /tmp

# Install dependencies
RUN apt-get update \
    && apt-get install -y libnet-ssleay-perl openssl libauthen-pam-perl libpam-runtime libio-pty-perl python

RUN rm /etc/apt/apt.conf.d/docker-gzip-indexes \
    && apt-get purge apt-show-versions \
    && rm /var/lib/apt/lists/*lz4 \
    && apt-get -o Acquire::GzipIndexes=false update \
    && apt-get install -y apt-show-versions

RUN wget http://prdownloads.sourceforge.net/webadmin/webmin_1.${WEBMIN_VERSION}_all.deb \
  && dpkg --install webmin_1.${WEBMIN_VERSION}_all.deb
