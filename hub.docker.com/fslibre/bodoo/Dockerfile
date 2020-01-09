FROM bitnami/minideb-extras:stretch-r401
LABEL maintainer "FS Libre <damendieta@fslibre.com>"

# Install required system packages and dependencies
RUN install_packages ghostscript imagemagick libbsd0 libbz2-1.0 libc6 libedit2 libffi6 libgcc1 libgcrypt20 libgmp10 libgnutls30 libgpg-error0 libhogweed4 libicu57 libidn11 libldap-2.4-2 liblzma5 libncurses5 libnettle6 libp11-kit0 libpq5 libreadline7 libsasl2-2 libsqlite3-0 libssl1.1 libstdc++6 libtasn1-6 libtinfo5 libxml2 libxslt1.1 zlib1g
RUN bitnami-pkg install python-3.6.8-2 --checksum 2eb057ee7701667327f6bcc1fc8765abe5d9d003a64124e5f8505fa692e71eb8
RUN bitnami-pkg install postgresql-client-11.4.0-0 --checksum 39c430fe23aef65ef26ca6f3cdd3758991ab25dff5e5c3bc2e4864d7b23ce2d3
RUN bitnami-pkg install node-7.10.1-1 --checksum 53362288e961d298a724353710a31901d4cb8237894a26a2f676b35450c02975
RUN bitnami-pkg unpack odoo-12.0.20190615-0 --checksum cd8369bf1d7687ec8bb11564ca630796ae256f70daa76ca12cf990a973386ad2

RUN apt-get update
RUN set -x; \
    apt-get install -y --no-install-recommends \
        apt-utils \
        vim \
        nano \
        wget \
        git \
        mc \
        fontconfig \
        xfonts-75dpi \
        xfonts-base \
        libxrender1 \
        xvfb \
        python-requests \
        python-unicodecsv \
        libxml2-dev \
        libxmlsec1-dev \
        python3-lasso \
        libffi-dev \
        python-dev \
        libldap2-dev \
        libsasl2-dev \
        libssl-dev \
        build-essential \
        python3-pandas \
        default-jdk \
        default-jre

RUN wget http://archive.ubuntu.com/ubuntu/pool/main/libj/libjpeg-turbo/libjpeg-turbo8_2.0.0-0ubuntu2_amd64.deb && dpkg -i libjpeg-turbo8_2.0.0-0ubuntu2_amd64.deb
RUN wget http://archive.ubuntu.com/ubuntu/pool/main/libp/libpng/libpng12-0_1.2.54-1ubuntu1_amd64.deb && dpkg -i libpng12-0_1.2.54-1ubuntu1_amd64.deb
RUN wget http://security.debian.org/debian-security/pool/updates/main/o/openssl/libssl1.0.0_1.0.1t-1+deb8u11_amd64.deb && dpkg -i libssl1.0.0_1.0.1t-1+deb8u11_amd64.deb
RUN wget https://github.com/wkhtmltopdf/wkhtmltopdf/releases/download/0.12.1/wkhtmltox-0.12.1_linux-trusty-amd64.deb && dpkg -i wkhtmltox-0.12.1_linux-trusty-amd64.deb

COPY rootfs /
ENV BITNAMI_APP_NAME="odoo" \
    BITNAMI_IMAGE_VERSION="12.0.20190615-debian-9-r10" \
    ODOO_EMAIL="user@example.com" \
    ODOO_PASSWORD="bitnami" \
    PATH="/opt/bitnami/python/bin:/opt/bitnami/postgresql/bin:/opt/bitnami/node/bin:$PATH" \
    POSTGRESQL_HOST="postgresql" \
    POSTGRESQL_PASSWORD="" \
    POSTGRESQL_PORT_NUMBER="5432" \
    POSTGRESQL_USER="postgres" \
    SMTP_HOST="" \
    SMTP_PASSWORD="" \
    SMTP_PORT="" \
    SMTP_PROTOCOL="" \
    SMTP_USER=""

RUN pip3 install --upgrade pip

RUN pip3 install \
        pyotp \
        unidecode \
        wand \
        checksumdir \
        num2words \
        cachetools \
        validate_email \
        phonenumbers \
        simplejson \
        oauthlib \
        pyqrcode \ 
        pyldap \
        zeep \
        xmltodict \
        odoorpc \
        openupgradelib \
        openpyxl \
        pyzk \
        viivakoodi \
        raven \
        email_validator

RUN pip install redis
RUN python3 -m pip install paramiko

EXPOSE 8069 8071

ENTRYPOINT [ "/app-entrypoint.sh" ]
CMD [ "nami", "start", "--foreground", "odoo" ]

