FROM rodrigozc/consul:1.0.3

LABEL author.name="Rodrigo Zampieri Castilho"
LABEL author.email="rodrigo.zampieri@gmail.com"
LABEL repository.url="https://bitbucket.org/rcastilho/kong-dashboard"

ENV NODEJS_VERSION "8"
ENV KONG_DASHBOARD_VERSION "v3.0.1"

ENV APPLICATION_DEFAULT_NAME "kong-dashboard"
ENV KONG_DEFAULT_ADMIN_PROTOCOL "http"
ENV KONG_DEFAULT_ADMIN_HOST "kong"
ENV KONG_DEFAULT_ADMIN_PORT "8001"

RUN apt-get update \
    && apt-get install -y --no-install-recommends openssl libpcre3 procps perl curl netcat-openbsd gnupg2 dirmngr \
    && wget --no-check-certificate -O nodesource_setup.sh https://deb.nodesource.com/setup_${NODEJS_VERSION}.x \
    && chmod +x nodesource_setup.sh \
    && ./nodesource_setup.sh \
    && rm nodesource_setup.sh \
    && apt-get install -y --no-install-recommends nodejs \
    && npm install -g kong-dashboard@${KONG_DASHBOARD_VERSION} \
    && apt-get clean \
    && rm -rf /var/lib/apt/lists/* /tmp/* /var/tmp/* /var/cache/*

ADD consul-template/1-consul-template.list /etc/consul-template/
ADD consul/service.ctmpl /etc/consul/
ADD consul/service.json /etc/consul/
ADD run/kong-dashboard.sh /docker/run/
