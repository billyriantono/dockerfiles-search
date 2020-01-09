FROM debian:stretch

LABEL maintainer="technical@brainbeanapps.com"

# Switch to root
USER root

# Use bash instead of sh (see https://github.com/eromoe/docker/commit/7dccc72bb24c715f176e4980ab59fd7aeb149a5f)
RUN rm /bin/sh && ln -s /bin/bash /bin/sh

# There's no terminal attached
ARG DEBIAN_FRONTEND=noninteractive

# Set the locale
RUN apt-get update \
  && apt-get install -y --no-install-recommends locales \
  && apt-get install -y --no-install-recommends locales-all \
  && apt-get clean \
  && rm -rf /var/lib/apt/lists/*
ENV LANG=C.UTF-8
ENV LANGUAGE=C.UTF-8
ENV LC_ALL=C.UTF-8
RUN locale-gen C.UTF-8 && update-locale LANG=C.UTF-8

# Install dependencies
RUN apt-get update \
  && apt-get install -y --no-install-recommends \
    apt-utils \
    wget \
    curl \
    dirmngr \
    gnupg \
    zip \
    xz-utils \
    ca-certificates \
    apt-transport-https \
    node-less \
    python3-pip \
    python3-setuptools \
    python3-renderpm \
    python3-watchdog \
    libssl1.0-dev \
  && apt-get clean \
  && rm -rf /var/lib/apt/lists/* \
  && pip3 install --upgrade pip

# Install dependency: postgresql-client
RUN echo 'deb http://apt.postgresql.org/pub/repos/apt/ stretch-pgdg main' > /etc/apt/sources.list.d/pgdg.list \
  && curl -sSL https://www.postgresql.org/media/keys/ACCC4CF8.asc | apt-key add - \
  && apt-get update  \
  && apt-get install -y postgresql-client \
  && rm -rf /var/lib/apt/lists/*

# Install dependency: wkhtmltopdf
RUN curl -o wkhtmltox.deb -sSL https://github.com/wkhtmltopdf/wkhtmltopdf/releases/download/0.12.5/wkhtmltox_0.12.5-1.stretch_amd64.deb \
  && echo '7e35a63f9db14f93ec7feeb0fce76b30c08f2057 wkhtmltox.deb' | sha1sum -c - \
  && dpkg --force-depends -i wkhtmltox.deb \
  && apt-get update \
  && apt-get -y install -f --no-install-recommends \
  && apt-get clean \
  && rm -rf /var/lib/apt/lists/* wkhtmltox.deb

# Install dependency: python3-ldap
RUN apt-get update \
  && apt-get install -y --no-install-recommends \
    build-essential \
    python3-dev \
    libldap2-dev \
    libsasl2-dev \
  && apt-get install -y --no-install-recommends \
    libldap-2.4-2 \
    libsasl2-2 \
  && pip3 install python-ldap \
  && apt-get remove -y \
    build-essential \
    python3-dev \
    libldap2-dev \
    libsasl2-dev \
  && apt-get autoremove -y \
  && apt-get clean \
  && rm -rf /var/lib/apt/lists/*

# Install dependency: python3-vobject
RUN pip3 install vobject

# Install dependency: python3-qrcode
RUN pip3 install qrcode

# Install dependency: num2words
RUN pip3 install num2words

# Install dependency: xlwt
RUN pip3 install xlwt

# Install dependency: xlsxwriter
RUN pip3 install xlsxwriter

# Install dependency: xlrd
RUN pip3 install xlrd

# Install dependency: phonenumbers
RUN pip3 install phonenumbers

# Install dependency: PyPDF2
RUN pip3 install PyPDF2

# Install dependency: py3o.template
RUN pip3 install py3o.template

# Install dependency: py3o.formats
RUN pip3 install py3o.formats

# Install dependency: requests
RUN pip3 install 'requests==2.21.0'

# Install dependency: jira
RUN pip3 install 'jira==2.0.0'

# Install dependency: oauthlib
RUN pip3 install 'oauthlib==2.1.0'

# Install dependency: requests-oauthlib
RUN pip3 install 'requests-oauthlib==1.1.0'

# Install dependency: requests-toolbelt
RUN pip3 install 'requests-toolbelt==0.9.1'

# Install dependency: PyJWT
RUN pip3 install 'PyJWT==1.7.1'

# Install dependency: cryptography
RUN pip3 install 'cryptography==2.6.1'

# Install dependency: bokeh
RUN pip3 install 'bokeh==0.12.7'

# Install dependency: openupgradelib
# RUN pip3 install openupgradelib
RUN pip3 install https://github.com/OCA/openupgradelib/archive/master.zip

# Install dependency: python3-lasso
RUN apt-get update \
  && apt-get install -y --no-install-recommends \
    python3-lasso \
  && apt-get clean \
  && rm -rf /var/lib/apt/lists/*

# Install depedency: fonts-noto-cjk + rtlcss
RUN echo 'deb http://deb.nodesource.com/node_10.x stretch main' > /etc/apt/sources.list.d/nodesource.list \
  && curl -sSL https://deb.nodesource.com/gpgkey/nodesource.gpg.key | apt-key add - \
  && apt-get update \
  && apt-get install -y nodejs fonts-noto-cjk \
  && npm install -g rtlcss \
  && apt-get clean \
  && rm -rf /var/lib/apt/lists/*

# Install Odoo
ENV ODOO_VERSION 12.0
ENV ODOO_RELEASE 20190805
RUN curl -o odoo.deb -sSL http://nightly.odoo.com/${ODOO_VERSION}/nightly/deb/odoo_${ODOO_VERSION}.${ODOO_RELEASE}_all.deb \
  && echo 'f173e34985524474d76fb37e47db2506531d76ba odoo.deb' | sha1sum -c - \
  && dpkg --force-depends -i odoo.deb \
  && apt-get update \
  && apt-get -y install -f --no-install-recommends \
  && apt-get clean \
  && rm -rf /var/lib/apt/lists/* odoo.deb

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
