FROM debian:stretch
MAINTAINER Douglas  <lambertinny.android@gmail.com>

# Generate locale C.UTF-8 for postgres and general locale data
ENV LANG C.UTF-8

# Install some deps, lessc and less-plugin-clean-css, and wkhtmltopdf
RUN set -x; \
        apt-get update \
        && apt-get install -y --no-install-recommends \
            #libxmlsec1-dev \
            #libxmlsec1-openssl \
            build-essential \
            ca-certificates \
            curl \
            libssl1.0-dev \
            libxml2-dev \
            node-less \
            python3-dev \
            python3-pip \
            python3-pyldap \
            python3-qrcode \
            python3-renderpm \
            python3-setuptools \
            python3-vobject \
            python3-watchdog \
            xmlsec1 \
            xz-utils \
        && curl -o wkhtmltox.deb -SL https://github.com/wkhtmltopdf/wkhtmltopdf/releases/download/0.12.5/wkhtmltox_0.12.5-1.stretch_amd64.deb \
        && echo '7e35a63f9db14f93ec7feeb0fce76b30c08f2057 wkhtmltox.deb' | sha1sum -c - \
        && dpkg --force-depends -i wkhtmltox.deb\
        && apt-get -y install -f --no-install-recommends \
        && rm -rf /var/lib/apt/lists/* wkhtmltox.deb

# Install Odoo
ENV ODOO_VERSION 13.0
ARG ODOO_RELEASE=20191011

RUN set -x; \
        curl -o odoo.deb -SL http://nightly.odoo.com/${ODOO_VERSION}/nightly/deb/odoo_${ODOO_VERSION}.${ODOO_RELEASE}_all.deb \
        && echo 'cf38e07f0a675b8d3d84578e6d53c701fd4d64e5 odoo.deb' | sha1sum -c - \
        && dpkg --force-depends -i odoo.deb \
        && apt-get update \
        && apt-get -y install -f --no-install-recommends \
        && rm -rf /var/lib/apt/lists/* odoo.deb


# Fix xmlsec
RUN  set -x; \ 
            apt-get update \
            && apt-get install -y --no-install-recommends \
                    libxml2-dev \
                    libxmlsec1-dev \
                    libxmlsec1-openssl \
            && rm -rf /var/lib/apt/lists/*

RUN pip3 install --no-cache-dir \
            lxml==4.2.3 \
            num2words \
            ofxparse==0.16 \
            phonenumbers \
            pillow==3.4.2 \
            pycnab240 \
            python3-boleto \
            python3-cnab \
            pytrustnfe3>=0.10.0 \
            Shapely==1.6.4.post2 \
            suds-jurko-requests \
            wheel \
            xlwt \ 
            xmlsec

# Copy entrypoint script and Odoo configuration file
COPY ./entrypoint.sh /
COPY ./odoo.conf /etc/odoo/
RUN chown odoo /etc/odoo/odoo.conf

# Mount /var/lib/odoo to allow restoring filestore and /mnt/extra-addons for users addons
RUN mkdir -p /mnt/extra-addons \
        && chown -R odoo /mnt/extra-addons
VOLUME ["/var/lib/odoo", "/mnt/extra-addons"]

# Expose Odoo services
EXPOSE 8069 8071

# Set the default config file
ENV ODOO_RC /etc/odoo/odoo.conf

# Set default user when running the container
USER odoo

ENTRYPOINT ["/entrypoint.sh"]
CMD ["odoo"]
