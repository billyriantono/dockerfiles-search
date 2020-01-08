FROM node:10-alpine

ARG VERSION=3.2.3

LABEL version=$VERSION

VOLUME ["/gitbook"]

WORKDIR /gitbook

RUN yarn global add gitbook-cli && \
    gitbook fetch ${VERSION} && \
    yarn cache clean && \
    rm -rf /tmp/* && \
    sed -i.bak 's/confirm: true/confirm: false/g' \
    /root/.gitbook/versions/${VERSION}/lib/output/website/copyPluginAssets.js

EXPOSE 4000

ENTRYPOINT [ "/usr/local/bin/gitbook" ]
