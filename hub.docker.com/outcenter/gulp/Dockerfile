FROM fedora:latest

RUN curl --silent --location https://rpm.nodesource.com/setup_10.x | bash -
RUN dnf -y install \
    git \
    nodejs \
    libpng-devel \
    make \
    gcc \
    gcc-c++ \
    patch

ENV TINI_VERSION v0.18.0
ADD https://github.com/krallin/tini/releases/download/${TINI_VERSION}/tini /sbin/tini
RUN chmod +x /sbin/tini

RUN mkdir /.npm
RUN chmod 777 -R /.npm

RUN npm install gulp-cli -g

COPY docker-entrypoint.sh /docker-entrypoint.sh
RUN chmod +x /docker-entrypoint.sh

WORKDIR /app

ENTRYPOINT ["/bin/sh", "/docker-entrypoint.sh"]

CMD ["gulp"]