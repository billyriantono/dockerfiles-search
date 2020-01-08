FROM ubuntu:trusty
MAINTAINER Renzo Meister <rm@jamotion.ch>

# Install PostgreSQL
ENV PG_VERSION=9.4 \
    PG_USER=postgres \
    USERMAP_GID=5050 \
    USERMAP_UID=5050 \
    PG_HOME="/var/lib/postgresql"

ENV PG_CONFDIR="/etc/postgresql/${PG_VERSION}/main" \
    PG_BINDIR="/usr/lib/postgresql/${PG_VERSION}/bin" \
    PG_DATADIR="${PG_HOME}/${PG_VERSION}/main"

RUN apt-get update && apt-get install -y --force-yes wget
RUN wget --quiet -O - https://www.postgresql.org/media/keys/ACCC4CF8.asc | apt-key add - \
 && echo 'deb http://apt.postgresql.org/pub/repos/apt/ trusty-pgdg main' > /etc/apt/sources.list.d/pgdg.list \
 && apt-get update \
 && apt-get install -y postgresql-${PG_VERSION} postgresql-client-${PG_VERSION} postgresql-contrib-${PG_VERSION} \
 && rm -rf ${PG_HOME} \
 && rm -rf /var/lib/apt/lists/*

# Install some deps, lessc and less-plugin-clean-css, and wkhtmltopdf
RUN apt-get update 
RUN apt-get install -y --no-install-recommends \
    ca-certificates curl nodejs npm python-support python-pyinotify  python-pip wget git fonts-dejavu poppler-utils antiword \
    && npm install -g less less-plugin-clean-css \
    && ln -s /usr/bin/nodejs /usr/bin/node \
    && curl -o wkhtmltox.deb -SL http://download.gna.org/wkhtmltopdf/0.12/0.12.1/wkhtmltox-0.12.1_linux-trusty-amd64.deb \
    && echo '7dd0e9be7e4fa2a58aa7066460927cdb8ba07492 wkhtmltox.deb' | sha1sum -c - \
    && dpkg --force-depends -i wkhtmltox.deb \
    && apt-get -y install -f --no-install-recommends \
    && apt-get purge -y --auto-remove -o APT::AutoRemove::RecommendsImportant=false -o APT::AutoRemove::SuggestsImportant=false npm \
    && rm -rf /var/lib/apt/lists/* wkhtmltox.deb

# Add PostgreSQL 9.4 source
RUN apt-get install -y --no-install-recommends wget && sh -c 'echo "deb http://apt.postgresql.org/pub/repos/apt/ $(lsb_release -cs)-pgdg main" > /etc/apt/sources.list.d/pgdg.list' \
    && wget --quiet -O - https://www.postgresql.org/media/keys/ACCC4CF8.asc | sudo apt-key add - \
    && apt-get update

# Install NGINX
RUN wget -O - http://nginx.org/keys/nginx_signing.key | sudo apt-key add - \
    && echo "deb http://nginx.org/packages/mainline/ubuntu/ trusty nginx" > /etc/apt/sources.list.d/nginx.list \
    && echo "deb-src http://nginx.org/packages/mainline/ubuntu/ trusty nginx" >> /etc/apt/sources.list.d/nginx.list \
    && apt-get update \
    && apt-get install nginx

# We set the odoo user and group fixed for compatibility with hosts
RUN addgroup --gid=5000 odoo && adduser --system --uid=5000 --gid=5000 --home /var/lib/odoo --shell /bin/bash odoo

# Install Odoo
ENV ODOO_VERSION 8.0
ENV ODOO_RELEASE 20160207

RUN set -x; \
        curl -o odoo.deb -SL http://nightly.odoo.com/${ODOO_VERSION}/nightly/deb/odoo_${ODOO_VERSION}.${ODOO_RELEASE}_all.deb \
        && dpkg --force-depends -i odoo.deb \
        && apt-get -y install -f --no-install-recommends \
        && rm -rf /var/lib/apt/lists/* odoo.deb

# Install gevent dependencies for running odoo with workers
RUN apt-get update
RUN apt-get install -y libevent-dev python-all-dev python-gevent python-psycopg2 python-matplotlib font-manager
RUN wget https://pypi.python.org/packages/source/p/psycogreen/psycogreen-1.0.tar.gz \
    && tar xvvf psycogreen-1.0.tar.gz \
    && cd psycogreen-1.0 \
    && python setup.py install \
    && easy_install greenlet \
    && easy_install gevent-psycopg2 \
    && easy_install PyWebDAV \
    && pip install gdata unidecode unirest ftputil xlrd docker-py pyserial \  
    && cd .. \
    && rm -rf psycogreen-1.0*

RUN chown -R odoo.odoo /usr/lib/python2.7/dist-packages/openerp

# Install aeroolib for Aeroo Reports
RUN pip install git+https://github.com/aeroo/aeroolib.git@master

# Install and configure OpenSSH Server (for development mode only)
RUN apt-get update && DEBIAN_FRONTEND=noninteractive apt-get -y install openssh-server pwgen
RUN mkdir -p /var/run/sshd \
    && sed -i "s/UsePrivilegeSeparation.*/UsePrivilegeSeparation no/g" /etc/ssh/sshd_config \
    && sed -i "s/UsePAM.*/UsePAM no/g" /etc/ssh/sshd_config \
    && sed -i "s/PermitRootLogin.*/PermitRootLogin yes/g" /etc/ssh/sshd_config

RUN locale-gen fr_FR \
    && locale-gen en_US.UTF-8 \
    && dpkg-reconfigure locales \
    && update-locale LANG=en_US.UTF-8 \
    && update-locale LC_ALL=en_US.UTF-8 \
    && echo 'LANG="en_US.UTF-8"' > /etc/default/locale

ADD bin /opt/odoo/bin

COPY bin/start /start
RUN chmod 755 /start

ENV AUTHORIZED_KEYS **None**
VOLUME ["/opt/odoo/custom_addons", "/opt/odoo/data", "/usr/local/share/fonts", "/etc/odoo", "/var/log/odoo"]

# Expose Odoo services
EXPOSE 2022 8069 8071 8072

# Set the default config file
ENV OPENERP_SERVER /etc/odoo/odoo-server.conf

ENTRYPOINT ["/start"]
