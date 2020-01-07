FROM alpine:3.8
LABEL maintainer="TRE-PR/SECTI/COSIS/Seção de Desenvolvimento de Sistemas <sds@tre-pr.jus.br>" \
      description="Imagem docker base alpine"

USER root

# Add TRE-PR CA root certificate and update trusted
COPY --chown=root:root tre-root-v2.crt /usr/local/share/ca-certificates/tre-root-v2.crt

# Install base packages
RUN apk update \
    && apk upgrade \
    && apk add --no-cache \
        ca-certificates tar unzip shadow curl\
    && update-ca-certificates
