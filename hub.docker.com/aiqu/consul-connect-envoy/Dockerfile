ARG CONSUL_VERSION=1.5.1
ARG ENVOY_VERSION=v1.9.1

# ------------------------------------------------------------------------------

FROM consul:${CONSUL_VERSION} AS source

# ------------------------------------------------------------------------------

FROM envoyproxy/envoy:${ENVOY_VERSION}

COPY --from=source ["/usr/bin/dumb-init","/bin/consul","/usr/bin/"]

ENTRYPOINT ["/usr/bin/dumb-init","/usr/bin/consul","connect"]
CMD ["-help"]
