FROM eclipse/ubuntu_python

MAINTAINER TP Sistemas S.A. <info@tpsistemas.com.ar>

# Generate locale C.UTF-8 for postgres and general locale data
ENV LANG C.UTF-8

WORKDIR /tmp

# Install some deps, lessc and less-plugin-clean-css, and wkhtmltopdf
RUN set -x; \
        sudo apt-get update \
        && sudo apt-get install -y --no-install-recommends \
            ca-certificates \
            curl \
            node-less \
            libssl-dev \
            libldap2-dev \
            libsasl2-dev \
            xz-utils \
        && curl -o wkhtmltox.tar.xz -SL https://github.com/wkhtmltopdf/wkhtmltopdf/releases/download/0.12.4/wkhtmltox-0.12.4_linux-generic-amd64.tar.xz \
        && echo '3f923f425d345940089e44c1466f6408b9619562 wkhtmltox.tar.xz' | sha1sum -c - \
        && tar xvf wkhtmltox.tar.xz \
        && sudo cp wkhtmltox/lib/* /usr/local/lib/ \
        && sudo cp wkhtmltox/bin/* /usr/local/bin/ \
        && sudo cp -r wkhtmltox/share/man/man1 /usr/local/share/man/

# Install Odoo
ENV ODOO_VERSION 11.0
ENV ODOO_RELEASE latest
RUN set -x; \
        curl -o odoo.deb -SL http://nightly.odoo.com/${ODOO_VERSION}/nightly/deb/odoo_${ODOO_VERSION}.${ODOO_RELEASE}_all.deb \
        && sudo dpkg --force-depends -i odoo.deb \
        && sudo apt-get update \
        && sudo apt-get -y install -f --no-install-recommends \
        && sudo rm -rf /var/lib/apt/lists/* odoo.deb

# Install Python dependencies
RUN sudo pip3 install num2words xlwt qrcode vobject

# Mount /var/lib/odoo to allow restoring filestore
VOLUME ["/var/lib/odoo"]
