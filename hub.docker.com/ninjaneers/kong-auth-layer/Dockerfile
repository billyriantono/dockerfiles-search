FROM kong

LABEL maintainer="info@ninjaneers.de"
LABEL "author"="Dmitrij Funkner"
LABEL "company"="Ninjaneers GmbH"

ENV KONG_VERSION 1.4.0

RUN luarocks install kong-opa && luarocks install kong-oidc
