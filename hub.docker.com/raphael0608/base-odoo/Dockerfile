FROM debian:stretch

LABEL version="1.1" \
    maintainer="Raphael Rodrigues<raphael0608@gmail.com>" \
    description="Odoo Base - Docker Container"

CMD ["/srv/odoo/bin/odoo"]

ENV ODOO_ADDONS_PATH="src/odoo/odoo/addons,src/odoo/addons" \
    ODOO_VERSION=11.0 \
    ODOO_DB_HOST=odoo \
    ODOO_DB_NAME=odoodb \
    ODOO_DB_FILTER=odoodb$ \
    ODOO_DB_USER=odoo \
    ODOO_DB_PASSWORD=odoo \
    ODOO_DB_PORT=5432 \
    ODOO_LIST_DB=False \
    LANG=C.UTF-8 \
    LC_ALL=C.UTF-8

VOLUME ["/filestore"]

WORKDIR /srv/odoo

RUN mkdir local bin && \
    apt-get update && \
    apt-get install -y \
    fontconfig \
    libfreetype6 \
    libx11-6 \
    libxext6 \
    libxrender1 \
    node-clean-css \
    node-less \
    python3-pip \
    virtualenv \
    python3.5 \
    wget \
    xfonts-75dpi \
    xfonts-base \
    xz-utils \
    zlib1g \
    gcc \
    libevent-dev \
    libjpeg-dev \
    libldap2-dev \
    libpng-dev \
    libpq-dev \
    libsasl2-dev \
    libxml2-dev \
    libxslt1-dev \
    python3.5-dev \
    gcc \
    g++ \
    libevent-dev \
    libjpeg-dev \
    libldap2-dev \
    libpng-dev \
    libpq-dev \
    libsasl2-dev \
    libxml2-dev \
    libxslt1-dev \
    python3.5-dev \
    wget \
    xz-utils \
    git

# Clone Odoo
RUN git clone -b 11.0 --depth=1 https://github.com/odoo/odoo /srv/odoo/src/odoo

# Install Wkhtmltopdf
RUN wget -qO wkhtmltox.tar.xz \
    https://github.com/wkhtmltopdf/wkhtmltopdf/releases/download/0.12.4/wkhtmltox-0.12.4_linux-generic-amd64.tar.xz && \
    tar -xf wkhtmltox.tar.xz && \
    install wkhtmltox/lib/* /usr/lib && \
    install wkhtmltox/bin/* /usr/bin && \
    rm -rf wkhtmltox wkhtmltox.tar.xz

# Install python pakages odoo
RUN pip3 install --no-cache-dir -r src/odoo/requirements.txt

# Clean
RUN apt-get remove --purge --autoremove -y && \
    apt-get clean;

COPY . /srv/odoo
RUN mv bin/docker-entrypoint.sh bin/odoo
