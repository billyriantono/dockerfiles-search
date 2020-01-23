FROM buildpack-deps:bionic
RUN apt-key adv --keyserver keyserver.ubuntu.com --recv-keys BF36996C4E1F8A59
COPY --chown=root:root *.list /etc/apt/sources.list.d/
# hadolint ignore=DL3008,DL3015
RUN apt-get update && \
    DEBIAN_FRONTEND=noninteractive apt-get dist-upgrade -y --auto-remove --purge && \
    DEBIAN_FRONTEND=noninteractive apt-get install -y \
        elementary-sdk \
    && \
    rm -rf /tmp/* /var/tmp/* /var/lib/apt/lists/* /var/cache/apt/archives/* /etc/ssl/certs/ssl-cert-snakeoil.pem /etc/ssl/private/ssl-cert-snakeoil.key
