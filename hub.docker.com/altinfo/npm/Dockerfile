FROM fedora:latest

LABEL maitainer="Luiz Fernando Pereira <luizfernandopereira@outlook.com.br>" \
      company="Alternativa Informática"

RUN dnf -y install \
    git \
    nodejs \
    libpng-devel \
    make \
    gcc \
    gcc-c++ \
    patch && dnf clean all

ENV TINI_VERSION v0.18.0
ADD https://github.com/krallin/tini/releases/download/${TINI_VERSION}/tini /sbin/tini
RUN chmod +x /sbin/tini

RUN mkdir /.npm
RUN chmod 777 -R /.npm

COPY entrypoint.sh /entrypoint.sh
RUN chmod +x /entrypoint.sh

WORKDIR /app

ENTRYPOINT ["/bin/sh", "/entrypoint.sh"]

CMD ["npm"]