FROM longinius/node

ENV IONIC_VERSION 5.4.2
ENV CORDOVA_VERSION 9.0.0

RUN npm install -g ionic@${IONIC_VERSION} && \
    npm install -g cordova@${CORDOVA_VERSION}

RUN ionic config set -g telemetry false && \
    cordova telemetry off