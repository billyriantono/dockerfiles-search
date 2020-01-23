FROM odoo:11.0

USER root

# Install dependencies
RUN apt-get update && apt-get install -y --no-install-recommends \
    libmagickwand-dev \
    python3.5 \
    python3-pip \
    python3-uno \
    ffmpeg \
    ghostscript \
    && \
    apt-get clean && \
    rm -rf /var/lib/apt/lists/*
    
RUN pip3 install Wand
RUN pip3 install cachetools
RUN pip3 install ez_setup
RUN pip3 install imageio
RUN pip3 install moviepy
RUN pip3 install odoo-autodiscover
RUN pip3 install odoo11-addon-base-location
RUN pip3 install xlrd
RUN pip3 install XlsxWriter
RUN pip3 install unoconv
RUN pip3 install phonenumbers
RUN pip3 install py-Asterisk
RUN pip3 install SOAPpy
RUN pip3 install checksumdir
RUN pip3 install raven
RUN pip3 install pysftp
RUN pip3 install acme-tiny
RUN pip3 install IPy
RUN pip3 install pyOpenSSL
