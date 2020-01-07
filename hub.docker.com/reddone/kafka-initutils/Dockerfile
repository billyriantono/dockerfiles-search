# same FROM as jre-zulu, to keep pull times down and to provide the same shell distro+version
FROM debian:stretch-slim@sha256:40b4072ce18fabe32f357f7c9ec1d256d839b1b95bcdc1f9c910823c6c2932e9

ENV KUBERNETES_CLIENT_VERSION=1.12.0-rc.2 \
    KUBERNETES_CLIENT_SHA256=306af04fc18ca2588e16fd831358df50a2cb02219687b543073836f835de8583

RUN set -ex; \
  export DEBIAN_FRONTEND=noninteractive; \
  runDeps='curl ca-certificates procps netcat'; \
  buildDeps=''; \
  apt-get update && apt-get install -y $runDeps $buildDeps --no-install-recommends; \
  rm -rf /var/lib/apt/lists/*; \
  \
  curl -sLS -o k.tar.gz -k https://dl.k8s.io/v${KUBERNETES_CLIENT_VERSION}/kubernetes-client-linux-amd64.tar.gz; \
  echo "$KUBERNETES_CLIENT_SHA256  k.tar.gz" | sha256sum -c; \
  tar -xvzf k.tar.gz -C /usr/local/bin/ --strip-components=3 kubernetes/client/bin/kubectl; \
  rm k.tar.gz; \
  \
  apt-get purge -y --auto-remove $buildDeps; \
  rm /var/log/dpkg.log /var/log/apt/*.log
