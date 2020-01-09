FROM kong:latest
RUN apk update && apk add git unzip curl
ENV KONG_PLUGINS="bundled, oidc"
RUN luarocks install kong-oidc