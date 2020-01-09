FROM alpine:3.8

LABEL vendor="Mintel" \
      maintainer="fciocchetti@mintel.com" \
      vcs-url="https://github.com/mintel/docker-alpine-satoshi-ci"

# versions
ENV PROMETHEUS_VERSION=2.4.3 \
    PROMETHEUS_SHA256=3aa063498ab3b4d1bee103d80098ba33d02b3fed63cb46e47e1d16290356db8a
ENV BASH_UNIT_VERSION=1.6.1 \
    BASH_UNIT_SHA256=596c2bcbcebcc5611e3f2e1458b0f4be1adad8f91498b20e97c9f7634416950f

# apk installs
RUN apk update --no-cache && \
    apk add --no-cache bash \
    curl \
    gawk \
    jq \
    make \
    python \
    py-pip \
    shadow \
    sed && \
    rm -rf /var/cache/apk/*

# pipsi install
RUN pip install yq && \
    pip install yamllint

WORKDIR /tmp

# promtool
RUN set -e \
    && curl -L https://github.com/prometheus/prometheus/releases/download/v${PROMETHEUS_VERSION}/prometheus-${PROMETHEUS_VERSION}.linux-amd64.tar.gz -o /tmp/prometheus.tar.gz \
    && echo "$PROMETHEUS_SHA256  prometheus.tar.gz" | sha256sum -c \
    && tar xzf /tmp/prometheus.tar.gz -C /tmp prometheus-${PROMETHEUS_VERSION}.linux-amd64/promtool \
    && mv /tmp/prometheus-${PROMETHEUS_VERSION}.linux-amd64/promtool /usr/local/bin/promtool \
    && rm /tmp/prometheus.tar.gz \
    && chmod +x /usr/local/bin/promtool

# bash_unit
RUN set -e \
    && curl -L https://github.com/pgrange/bash_unit/archive/v${BASH_UNIT_VERSION}.tar.gz -o /tmp/bash_unit.tar.gz \
    && echo "$BASH_UNIT_SHA256  bash_unit.tar.gz" | sha256sum -c \
    && tar zxvf /tmp/bash_unit.tar.gz  -C /tmp \
    && mv /tmp/bash_unit-${BASH_UNIT_VERSION}/bash_unit /usr/local/bin \
    && chmod a+x /usr/local/bin \
    && rm -f /tmp/bash_unit.tar.gz

# setup user
RUN useradd -ms /bin/bash mintel
USER mintel

ENTRYPOINT ["/bin/bash"]

