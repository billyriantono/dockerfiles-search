FROM ubuntu:14.04

# Nainstalovat potřebné balíčky
RUN apt-get update \
    && DEBIAN_FRONTEND=noninteractive apt-get install -y \
        libaio1 \
        unzip \
        rlwrap \
    && rm -rf /var/lib/apt/lists/*

# Rozbalit balíčky Oracle Instant Client
# Balíčky je možno stáhnout z http://www.oracle.com/technetwork/topics/linux-amd64-093390.html
COPY assets /tmp
WORKDIR /tmp
RUN unzip 'instantclient-*.zip' -d /opt \
    && rm -f *

# Nastavit požadované proměnné prostředí
ENV PATH /opt/instantclient_12_1:$PATH
ENV LD_LIBRARY_PATH /opt/instantclient_12_1

# Výchozí příkaz pro spuštění sqlplus
COPY docker-entrypoint.sh /
WORKDIR /
ENTRYPOINT ["/docker-entrypoint.sh"]
