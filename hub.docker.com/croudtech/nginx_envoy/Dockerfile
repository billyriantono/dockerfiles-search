FROM croudtech/nginx

# ENVOY INSTALLATION

ENV ENVOY_VERSION=1.1.0
RUN curl -L -O https://github.com/lyft/envoy/archive/v${ENVOY_VERSION}.zip
RUN unzip v${ENVOY_VERSION}.zip

RUN cd envoy-${ENVOY_VERSION} \
    && ls -la ci
