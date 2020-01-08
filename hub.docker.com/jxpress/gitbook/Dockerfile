FROM node:6-slim

ENV GITBOOK_VERSION 3.2.0

RUN apt-get update && apt-get install -y --no-install-recommends \
        git \
        calibre \
        fonts-ipaexfont-gothic && \
    npm install -g gitbook-cli && \
    gitbook fetch ${GITBOOK_VERSION} && \
    rm -rf /var/lib/apt/lists/* /root/.npm /tmp/npm*

ENTRYPOINT ["gitbook"]
