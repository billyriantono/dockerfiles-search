FROM rodrigozc/consul:1.0.3

LABEL author.name="Rodrigo Zampieri Castilho"
LABEL author.email="rodrigo.zampieri@gmail.com"
LABEL repository.url="https://bitbucket.org/rcastilho/kong"

ENV NODEJS_VERSION "8"
ENV KONG_VERSION "0.11.2"

ENV APPLICATION_DEFAULT_NAME "kong"

RUN apt-get update \
    && apt-get install -y --no-install-recommends openssl libpcre3 procps perl curl netcat-openbsd gnupg2 dirmngr \
    && curl -L https://kong.bintray.com/kong-community-edition-deb/dists/kong-community-edition-${KONG_VERSION}.jessie.all.deb -o kong-community-edition-${KONG_VERSION}.jessie.all.deb \
    && dpkg -i kong-community-edition-${KONG_VERSION}.jessie.all.deb \
    && rm kong-community-edition-${KONG_VERSION}.jessie.all.deb \
    && apt-get clean \
    && rm -rf /var/lib/apt/lists/* /tmp/* /var/tmp/* /var/cache/*

ADD consul-template/1-consul-template.list /etc/consul-template/
ADD consul/service.ctmpl /etc/consul/
ADD consul/service.json /etc/consul/
ADD run/kong.sh /docker/run/
