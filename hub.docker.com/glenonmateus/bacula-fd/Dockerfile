FROM debian:buster

ENV BACULA_VERSION 9.4.4
ENV DEBIAN_FRONTEND noninteractive
ENV TZ America/Sao_Paulo

RUN apt-get update \
    && apt-get install -y --no-install-recommends \
		curl \
		ca-certificates \
		make \
		build-essential \
		file \
    && apt clean && rm -rf /var/lib/apt/lists/* \
    && mkdir -p /etc/bacula /var/lib/bacula /run/bacula /etc/bacula/scripts \
    && useradd -U -s /bin/sh -d /var/lib/bacula bacula \
    && curl -sL https://sourceforge.net/projects/bacula/files/bacula/${BACULA_VERSION}/bacula-${BACULA_VERSION}.tar.gz/download -o bacula-${BACULA_VERSION}.tar.gz \
    && tar xzf bacula-${BACULA_VERSION}.tar.gz && cd bacula-${BACULA_VERSION} \
    && ./configure \
		--enable-smartalloc \
		--sbindir=/usr/bin/ \
		--sysconfdir=/etc/bacula/ \
		--with-pid-dir=/run/bacula/ \
		--with-subsys-dir=/var/lib/bacula \
		--with-working-dir=/var/lib/bacula \
		--with-scriptdir=/etc/bacula/scripts \
		--enable-client-only \
		--with-fd-user=bacula \
		--with-fd-group=bacula \
    && make && make install \
    && cd .. && rm -rf bacula-${BACULA_VERSION}*

EXPOSE 9102

COPY ["bacula-fd.conf","/etc/bacula/"]
COPY ["run", "/usr/local/bin"]
RUN chmod +x /usr/local/bin/run

VOLUME ["/etc/bacula/", "/var/lib/bacula"]

ENTRYPOINT ["/usr/local/bin/run"]
