FROM debian:stretch
MAINTAINER Victoria LV ltd. <vahe@vlv-pro.ru>
RUN set -x; \
	apt-get update \
	&& apt-get install -y \
	wget \
	apt-utils \
	postgresql-client \
	curl \
	python2.7 \
	nano \
	python-virtualenv \
	xz-utils \
	libx11-6 \
	libxcb1 \
	libxext6 \
	libxrender1 \
	xfonts-75dpi \
	xfonts-base \
	fontconfig \
	libjpeg62-turbo \
	python-pip
#INstall WKHTMLTOPDF
RUN curl -o wkhtmltox.deb -SL https://github.com/wkhtmltopdf/wkhtmltopdf/releases/download/0.12.5/wkhtmltox_0.12.5-1.stretch_amd64.deb \
        && echo '7e35a63f9db14f93ec7feeb0fce76b30c08f2057 wkhtmltox.deb' | sha1sum -c - \
        && dpkg --force-depends -i wkhtmltox.deb\
        && apt-get -y install -f --no-install-recommends
# RUN set -x; \	apt-get update\
#RUN set -x; \
#    echo 'deb http://apt.postgresql.org/pub/repos/apt/ stretch-pgdg main' >  /etc/apt/sources.list.d/pgdg.list \
#    wget --quiet -O - https://www.postgresql.org/media/keys/ACCC4CF8.asc | apt-key add -
RUN apt-get install -y\
	gcc \
	python2.7-dev \
	libxml2-dev \
	libxslt1-dev \
	libevent-dev \
	libsasl2-dev \
	libldap2-dev \
	libpq-dev \
	libpng-dev \
	libjpeg-dev \
	node-less \
	node-clean-css

### Install ODOO
ENV ODOO_VERSION 8.0
RUN adduser --system --quiet --shell=/bin/bash --home=/odoo --gecos 'ODOO' --group odoo
RUN set -x; \
    mkdir /odoo/log \
	/odoo/data-dir \
	/odoo/custom_addons \
	/odoo/odoo-config \
	/odoo/oca_addons

# Copy Odoo
ENV ODOO_VERSION 8.0
ENV ODOO_RELEASE 20171001
RUN set -x; \
    curl -o odoo.tar.gz http://nightly.odoo.com/${ODOO_VERSION}/nightly/src/odoo_${ODOO_VERSION}.${ODOO_RELEASE}.tar.gz \
    && tar -xzf odoo.tar.gz \
    && mv odoo-${ODOO_VERSION}-${ODOO_RELEASE} /odoo/odoo8 \
    && rm odoo.tar.gz
#COPY ./odoo /odoo/odoo8
RUN pip install -r /odoo/odoo8/requirements.txt
RUN rm -rf /var/lib/apt/lists/* wkhtmltox.deb \
	&& apt-get remove -y gcc \
	python-pip \
	&& apt-get autoremove -y
RUN chown odoo:odoo -R /odoo
USER odoo
CMD ["/odoo/odoo8/openerp-server", "-c", "/odoo/odoo-config/odoo.conf"]