FROM microsoft/aspnetcore-build:2.0.6-2.1.101-jessie

ARG VERSION=3.2.3

LABEL version=$VERSION

RUN npm install --global gitbook-cli \
        && gitbook fetch ${VERSION} \
        && npm cache clean --force \
        && rm -rf /tmp/*

CMD [“/bin/echo”, “Everything is OK”]
