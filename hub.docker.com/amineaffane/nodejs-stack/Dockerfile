FROM adoptopenjdk/openjdk13-openj9:jre-13_33_openj9-0.16.0-alpine

ARG NODE_VERSION=12.13.1-r0
ARG KUBECTL_VERSION=v1.16.3
ARG DOCKER_VERSION=19.03.5-r0
ARG CHROME_VERSION=78.0.3904.108-r0

LABEL nodejs.version=${NODE_VERSION}
LABEL kubectl.version=${KUBECTL_VERSION}
LABEL docker.version=${DOCKER_VERSION}
LABEL chrome.version=${CHROME_VERSION}

# non-root user
ARG GID=1000
ARG UID=1000
ARG ME=app
ARG HOME_DIR=/home/${ME}

LABEL default.user.uid=${UID}
LABEL default.user.gid=${GID}
LABEL default.user.name=${ME}
LABEL default.workdir=${HOME_DIR}

RUN addgroup -g ${GID} ${ME} \
    && adduser -D -u ${UID} -G ${ME} ${ME}

# Update and utility packages
RUN echo "http://dl-2.alpinelinux.org/alpine/edge/main" > /etc/apk/repositories \
    && echo "http://dl-2.alpinelinux.org/alpine/edge/community" >> /etc/apk/repositories \
    && echo "http://dl-2.alpinelinux.org/alpine/edge/testing" >> /etc/apk/repositories \
    && apk -U --no-cache --allow-untrusted add \
            curl

# Docker
RUN apk -U --no-cache --allow-untrusted add \
        docker=${DOCKER_VERSION}

# Chrome
ENV CHROME_BIN /usr/bin/chromium-browser

RUN apk -U --no-cache --allow-untrusted add \
        chromium-chromedriver=${CHROME_VERSION} \
        chromium=${CHROME_VERSION} \
        g++ \
        nss \
        freetype \
        freetype-dev \
        harfbuzz \
        ca-certificates \
        ttf-freefont

# NodeJS
RUN apk -U --no-cache --allow-untrusted add \
        nodejs=${NODE_VERSION} \
        npm=${NODE_VERSION}

# kubectl
RUN curl -LO https://storage.googleapis.com/kubernetes-release/release/${KUBECTL_VERSION}/bin/linux/amd64/kubectl \
    && chmod +x ./kubectl \
    && mv ./kubectl /usr/local/bin/kubectl

# cleanup
RUN apk del curl \
    && rm -rf /var/lib/apt/lists/* \
              /var/cache/apk/* \
              /usr/share/man \
              /tmp/*

USER app

WORKDIR ${HOME_DIR}
