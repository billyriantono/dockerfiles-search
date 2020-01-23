FROM grafana/grafana:5.4.2

USER root

RUN apt-get update \
    && apt-get install --yes --no-install-recommends \
       wget \
       unzip \
       ca-certificates \
    && apt-get clean \
    && rm -rf /var/lib/apt/lists/*

# Install dumb-init
ENV DUMB_INIT_VERSION 1.2.2
ENV DUMB_INIT_SHA256 37f2c1f0372a45554f1b89924fbb134fc24c3756efaedf11e07f599494e0eff9

RUN wget -q -O /usr/local/bin/dumb-init https://github.com/Yelp/dumb-init/releases/download/v${DUMB_INIT_VERSION}/dumb-init_${DUMB_INIT_VERSION}_amd64 \
    && echo "${DUMB_INIT_SHA256} /usr/local/bin/dumb-init" | sha256sum -c - \
    && chmod +x /usr/local/bin/dumb-init

# Install consul-template
ENV CONSUL_TEMPLATE_VERSION 0.19.5
ENV CONSUL_TEMPLATE_SHA256 e6b376701708b901b0548490e296739aedd1c19423c386eb0b01cfad152162af

RUN wget -q -O /tmp/consul-template.zip https://releases.hashicorp.com/consul-template/${CONSUL_TEMPLATE_VERSION}/consul-template_${CONSUL_TEMPLATE_VERSION}_linux_amd64.zip \
    && echo "${CONSUL_TEMPLATE_SHA256} /tmp/consul-template.zip" | sha256sum -c - \
    && gunzip -c /tmp/consul-template.zip > /usr/local/bin/consul-template \
    && chmod +x /usr/local/bin/consul-template \
    && rm /tmp/consul-template.zip

COPY docker-entrypoint.sh /docker-entrypoint.sh

ENTRYPOINT ["/docker-entrypoint.sh"]
CMD ["consul-template", "-config=/srv/consul-template.cfg"]

EXPOSE 3000

# Install the plugins in a non-standard place, since /var/lib/grafana is going
# to be overwritten at runtime due to being a Docker VOLUME.
ENV GF_PATHS_PLUGINS=/srv/grafana/plugins
RUN mkdir --parents ${GF_PATHS_PLUGINS} && chown grafana:grafana ${GF_PATHS_PLUGINS} && \
    grafana-cli --pluginsDir "${GF_PATHS_PLUGINS}" plugins install grafana-piechart-panel 1.2.0 && \
    grafana-cli --pluginsDir "${GF_PATHS_PLUGINS}" plugins install natel-discrete-panel 0.0.6
