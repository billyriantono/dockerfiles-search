FROM datadog/cluster-agent:1.3.2

ARG NODE_VERSION=node_10.x
ARG NODE_APT_KEY=68576280
ARG YARN_APT_KEY=86E50310

COPY ["templates/*.tmpl", "/opt/templates/"]

COPY scripts/ /usr/local/bin/

RUN apt-get update \
 # datadog image already has /etc/ssl/openssl.conf
 # use --force-conf-old to keep it
 && apt-get install -y \
                    -o Dpkg::Options::="--force-confdef" \
                    -o Dpkg::Options::="--force-confold" \
                    --no-install-recommends \
                    ca-certificates \
                    apt-transport-https \
                    gettext-base \
                    lsb-release \
                    gnupg \
 && export DISTRO="$(lsb_release -s -c)" \
 && envsubst < /opt/templates/500px.list.tmpl > /etc/apt/sources.list.d/500px.list \
 && apt-key adv --recv-keys --keyserver hkp://keyserver.ubuntu.com:80 \
      $NODE_APT_KEY \
      $YARN_APT_KEY \
 && apt-get update \
 && apt-get install -y \
                    --no-install-recommends \
                    nodejs \
                    yarn \
 && yarn global add kms-env@0.3.0 \
 && rm -rf /var/lib/apt/lists/*

ENTRYPOINT ["/usr/local/bin/bootstrap"]
CMD ["/entrypoint.sh", "datadog-cluster-agent", "start"]
