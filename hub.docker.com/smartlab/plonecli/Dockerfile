FROM python:2.7.15-alpine3.7 

RUN addgroup -g 500 plone \
 && adduser -S -D -G plone -u 500 plone \ 
 && mkdir /tmp/buildout \
 && chown plone:plone /tmp/buildout

COPY requirements.txt /tmp/

LABEL plone=plonecli \
    os="alpine" \
    os.version="3.7" \
    name="Plone for developers" \
    description="Plone Dev image to use in SmartLab Open Data Project" \
    maintainer="smartlab-dev@mpt.mp.br"

RUN apk add --no-cache --virtual .build-deps \
    gcc \
    bzip2-dev \
    libc-dev \
    ncurses-dev \
    openssl-dev \
    readline-dev \
    zlib-dev \
    libxml2-dev \
    libxslt-dev \
    libjpeg-turbo-dev \
    libpng-dev openssl \
    yaml-dev \
    poppler-dev \
    py2-virtualenv \
    sudo \
    make \
    curl 
RUN apk add --no-cache --virtual .run-deps \
    libbz2 \
    wv \
    bash \
    libxml2 \
    libxslt \
    libjpeg-turbo \
    git \
    rsync  
RUN pip install -r /tmp/requirements.txt \
 && find /usr -name buildout.cfg.bob | xargs sed -e '2iabi-tag-eggs = true' -i \
 && find /usr -name buildout.cfg.bob | xargs sed -e '2idownload-cache = /tmp/buildout/download-cache' -i \
 && find /usr -name buildout.cfg.bob | xargs sed -e '2ieggs-directory = /tmp/buildout/eggs' -i

VOLUME /tmp/buildout
WORKDIR /tmp/buildout
USER plone
EXPOSE 8080
