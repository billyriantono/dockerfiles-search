FROM whitecat29/apline-elixir-phoenix:latest
MAINTAINER William Tran <chitran.whitecat@gmail.com>

ENV TERM=xterm

RUN apk update && \
    apk --no-cache update add \
    libgcc libstdc++ libx11 glib-dev libxrender libxext libintl \
    libcrypto1.0 libssl1.0 \
    ttf-dejavu ttf-droid ttf-freefont ttf-liberation ttf-ubuntu-font-family \
    automake \
    bzip2 \
    bzip2-dev \
    curl-dev \
    db-dev \
    dpkg \
    dpkg-dev \
    file \
    g++ \
    gcc \
    gdbm-dev \
    geoip-dev \
    libxml2 \
    libxslt \
    bash \
    python \
    build-essential \
    rm -rf /var/cache/apk/*
    
COPY wkhtmltopdf /usr/bin

# try fix
RUN ln -s /bin/sh /bin/source

WORKDIR /opt/app

CMD ["/bin/sh"]
