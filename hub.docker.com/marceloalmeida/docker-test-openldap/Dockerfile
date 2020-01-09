FROM debian:stretch-slim
LABEL maintainer="Marcelo Almeida - github.com/marceloalmeida"

# Install slapd and requirements
RUN apt-get update \
    && DEBIAN_FRONTEND=noninteractive apt-get \
        install -y --no-install-recommends \
            slapd \
            ldap-utils \
            openssl \
            ca-certificates \
    && rm -rf /var/lib/apt/lists/* \
    && mkdir /etc/ldap/ssl /bootstrap

ENV LDAP_DEBUG_LEVEL=256

# ADD run script
COPY ./run.sh /run.sh

# ADD bootstrap files
ADD ./bootstrap /bootstrap

# Initialize LDAP with data
ARG DATASET=thesimpsons
RUN /bin/bash /bootstrap/slapd-init.sh ${DATASET}

VOLUME ["/etc/ldap/slapd.d", "/etc/ldap/ssl", "/var/lib/ldap", "/run/slapd"]

EXPOSE 389 636

CMD ["/bin/bash", "/run.sh"]
ENTRYPOINT []
