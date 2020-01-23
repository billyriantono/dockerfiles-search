# Use ubuntu 14.04 as main image
FROM ubuntu:14.04

RUN echo "deb http://http.debian.net/debian jessie-backports main" | \
tee -a /etc/apt/sources.list

# Install dependencies
RUN apt-get clean && apt-get update
RUN apt-get install -y --force-yes build-essential python-pip python-dev \
    libjpeg-dev libfreetype6 libfreetype6-dev \
    zlib1g-dev gettext libmysqlclient-dev wget \
    libcurl4-openssl-dev libssl-dev libffi-dev sqlite3 libpq-dev libgrpc-dev xvfb xorg

# Install wkhtmltopdf
RUN wget http://download.gna.org/wkhtmltopdf/0.12/0.12.2.1/wkhtmltox-0.12.2.1_linux-trusty-amd64.deb
RUN dpkg -i wkhtmltox-0.12.2.1_linux-trusty-amd64.deb
RUN apt-get -f install

RUN printf '#!/bin/bash\nxvfb-run -a --server-args="-screen 0, 1024x768x24" /usr/bin/wkhtmltopdf $*' > /usr/bin/wkhtmltopdf.sh
RUN chmod a+x /usr/bin/wkhtmltopdf.sh
RUN ln -s /usr/bin/wkhtmltopdf.sh /usr/local/bin/wkhtmltopdf
