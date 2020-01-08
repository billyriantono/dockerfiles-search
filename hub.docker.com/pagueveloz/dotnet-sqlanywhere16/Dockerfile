FROM mcr.microsoft.com/dotnet/core/sdk:3.0.100-preview7-bionic as base

WORKDIR /tmp

RUN set -xe \
  && DEVBUILD="\
    apt-utils \
    language-pack-en-base \
    curl \
    unzip \
    software-properties-common" \
  && PACOTES="\
  	tzdata \
    unixodbc" \
  && apt-get -y update \
  && DEBIAN_FRONTEND=noninteractive apt-get install -y $DEVBUILD --no-install-recommends --no-install-suggests \
  && DEBIAN_FRONTEND=noninteractive apt-get install -y $PACOTES --no-install-recommends --no-install-suggests \
  && echo "America/Sao_Paulo" | tee /etc/timezone \
  && ln -sf /usr/share/zoneinfo/America/Sao_Paulo /etc/localtime \
  && dpkg-reconfigure -f noninteractive tzdata \
  && mkdir -p /opt/sqlanywhere16 \
  && curl -L -O http://d5d4ifzqzkhwt.cloudfront.net/sqla16client/sqla16_client_linux_x86x64.tar.gz \
  && tar xzvf /tmp/sqla16_client_linux_x86x64.tar.gz -C /tmp \
  && /tmp/client1600/setup -silent -nogui -I_accept_the_license_agreement -sqlany-dir /opt/sqlanywhere16 \
  && apt-get purge -y --auto-remove -o APT::AutoRemove::RecommendsImportant=false $DEVBUILD \
  && apt-get clean autoclean \
  && rm -rf /opt/sqlanywhere16/bin* \
  && rm -rf /opt/sqlanywhere16/support \
  && rm -rf /opt/sqlanywhere16/java \
  && rm -rf /opt/sqlanywhere16/sdk \
  && rm -rf /opt/sqlanywhere16/samples \
  && rm -rf /opt/sqlanywhere16/deployment \
  && rm -rf /opt/sqlanywhere16/thirdpartylegal \
  && rm -rf /opt/sqlanywhere16/*.txt \
  && rm -rf /opt/sqlanywhere16/lib64/php* \
  && rm -rf /opt/sqlanywhere16/lib32 \
  && rm -rf /var/lib/{apt,dpkg,cache,log}/ \
  && rm -rf /var/lib/apt/lists/* /tmp/* /var/tmp/* \
  && echo "/opt/sqlanywhere16/lib64" >> /etc/ld.so.conf.d/sqlanywhere16.conf

ENV LD_LIBRARY_PATH=/opt/sqlanywhere16/lib64
ENV SQLANY16=/opt/sqlanywhere16
ENV PATH=$SQLANY16/bin64:${PATH:-}
ENV TZ=America/Sao_Paulo

