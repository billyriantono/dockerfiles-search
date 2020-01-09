# See CKAN docs on installation from Docker Compose on usage
FROM debian:jessie
MAINTAINER Open Knowledge

# Install required system packages
RUN apt-get -q -y update \
    && DEBIAN_FRONTEND=noninteractive apt-get -q -y upgrade \
    && apt-get -q -y install \
        python-dev \
        python-pip \
        python-virtualenv \
        python-wheel \
        libpq-dev \
        libxml2-dev \
        libxslt-dev \
        libgeos-dev \
        libssl-dev \
        libffi-dev \
        postgresql-client \
        build-essential \
        git-core \
        vim \
        wget \
    && apt-get -q clean \
    && rm -rf /var/lib/apt/lists/*

# Define environment variables
ENV CKAN_HOME /usr/lib/ckan
ENV CKAN_VENV $CKAN_HOME/venv
ENV CKAN_CONFIG /etc/ckan
ENV CKAN_STORAGE_PATH=/var/lib/ckan
ENV CKAN_SMTP_SERVER=mailhub.env.cz
ENV CKAN_MAX_UPLOAD_SIZE_MB=100


# Build-time variables specified by docker-compose.yml / .env
ARG CKAN_SITE_URL

# Create ckan user
RUN useradd -r -u 900 -m -c "ckan account" -d $CKAN_HOME -s /bin/false ckan

# Setup virtual environment for CKAN
RUN mkdir -p $CKAN_VENV $CKAN_CONFIG $CKAN_STORAGE_PATH && \
    virtualenv $CKAN_VENV && \
    ln -s $CKAN_VENV/bin/pip /usr/local/bin/ckan-pip &&\
    ln -s $CKAN_VENV/bin/paster /usr/local/bin/ckan-paster

# Setup CKAN
ADD . $CKAN_VENV/src/ckan/
RUN mv $CKAN_VENV/src/ckan/ckanext-mzp $CKAN_VENV/src
RUN mv $CKAN_VENV/src/ckan/ckanext-hierarchy $CKAN_VENV/src
RUN ckan-pip install -U pip && \
    ckan-pip install --upgrade --no-cache-dir -r $CKAN_VENV/src/ckan/requirement-setuptools.txt && \
    ckan-pip install --upgrade --no-cache-dir -r $CKAN_VENV/src/ckan/requirements.txt && \
    ckan-pip install -e $CKAN_VENV/src/ckan/ && \
    ckan-pip install -e "git+https://github.com/ckan/ckanext-spatial.git#egg=ckanext-spatial" && \
    ckan-pip install -r $CKAN_VENV/src/ckanext-spatial/pip-requirements.txt && \
    ckan-pip install -e "git+https://github.com/ckan/ckanext-dcat.git#egg=ckanext-dcat" && \
    ckan-pip install -r $CKAN_VENV/src/ckanext-dcat/requirements.txt && \
    ckan-pip install -e "git+https://github.com/ckan/ckanext-harvest.git#egg=ckanext-harvest" && \
    ckan-pip install -e "git+https://github.com/okfn/ckanext-disqus#egg=ckanext-disqus" && \
    ckan-pip install -e "git+https://github.com/ckan/ckanext-scheming.git#egg=ckanext-scheming" && \ 
    ckan-pip install ckanext-datarequests && \
    ckan-pip install -r $CKAN_VENV/src/ckanext-harvest/pip-requirements.txt && \
    ckan-pip install -e $CKAN_VENV/src/ckanext-mzp && \
    ckan-pip install -e $CKAN_VENV/src/ckanext-hierarchy && \
    ln -s $CKAN_VENV/src/ckan/ckan/config/who.ini $CKAN_CONFIG/who.ini && \
    cp -v $CKAN_VENV/src/ckan/contrib/docker/ckan-entrypoint.sh /ckan-entrypoint.sh && \
    chmod +x /ckan-entrypoint.sh && \
    chown -R ckan:ckan $CKAN_HOME $CKAN_VENV $CKAN_CONFIG $CKAN_STORAGE_PATH $CKAN_VENV/src/ckanext-spatial $CKAN_VENV/src/ckanext-hierarchy $CKAN_VENV/src/ckanext-dcat $CKAN_VENV/src/ckanext-harvest

ENTRYPOINT ["/ckan-entrypoint.sh"]

USER ckan
EXPOSE 5000

CMD ["ckan-paster","serve","/etc/ckan/production.ini"]
