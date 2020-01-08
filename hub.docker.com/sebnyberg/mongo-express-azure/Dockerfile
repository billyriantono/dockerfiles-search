FROM node:8

# grab tini for signal processing and zombie killing
# RUN set -x \
#   && apt-get update && apt-get install -y ca-certificates curl \
#   --no-install-recommends 

ENV TINI_VERSION v0.18.0
ADD https://github.com/krallin/tini/releases/download/${TINI_VERSION}/tini /usr/local/bin/tini
RUN chmod +x /usr/local/bin/tini
# && curl -fSL "https://github.com/krallin/tini/releases/download/v${TINI_VERSION}/tini" -o /usr/local/bin/tini \
# && curl -fSL "https://github.com/krallin/tini/releases/download/v${TINI_VERSION}/tini.asc" -o /usr/local/bin/tini.asc \
# && export GNUPGHOME="$(mktemp -d)" \
# && gpg --keyserver ha.pool.sks-keyservers.net --recv-keys 595E85A6B1B4779EA4DAAEC70B588DFF0527A9B7 \
# && gpg --batch --verify /usr/local/bin/tini.asc /usr/local/bin/tini \
# && gpg --batch --keyserver hkp://p80.pool.sks-keyservers.net:80 --recv-keys 595E85A6B1B4779EA4DAAEC70B588DFF0527A9B7 \
# && gpg --batch --verify /tini.asc /tini \
# && rm -r "$GNUPGHOME" /usr/local/bin/tini.asc \
# && chmod +x /usr/local/bin/tini \
# && tini -h \
# && apt-get purge --auto-remove -y ca-certificates curl \
# && rm -rf /var/lib/apt/lists/*

# ENV TINI_VERSION v0.18.0
# ADD https://github.com/krallin/tini/releases/download/${TINI_VERSION}/tini /tini
# ADD https://github.com/krallin/tini/releases/download/${TINI_VERSION}/tini.asc /tini.asc
# RUN gpg --batch --keyserver hkp://p80.pool.sks-keyservers.net:80 --recv-keys 595E85A6B1B4779EA4DAAEC70B588DFF0527A9B7 \
#   && gpg --batch --verify /tini.asc /tini

# ENV TINI_VERSION v0.18.0
# ADD https://github.com/krallin/tini/releases/download/${TINI_VERSION}/tini /tini
# ADD https://github.com/krallin/tini/releases/download/${TINI_VERSION}/tini /tini
# ADD https://github.com/krallin/tini/releases/download/${TINI_VERSION}/tini.asc /tini.asc


# override some config defaults with values that will work better for docker
# ENV ME_CONFIG_EDITORTHEME="default" \
#     ME_CONFIG_MONGODB_SERVER="mongo" \
#     ME_CONFIG_MONGODB_ENABLE_ADMIN="true" \
#     ME_CONFIG_BASICAUTH_USERNAME="" \
#     ME_CONFIG_BASICAUTH_PASSWORD="" \
#     VCAP_APP_HOST="0.0.0.0"
# ENV VCAP_PP_HOST="0.0.0.0"

WORKDIR /app

COPY . /app

RUN set -x \
  && apt-get update && apt-get install -y git --no-install-recommends \
  && npm install  \
  && apt-get purge --auto-remove -y git \
  && rm -rf /var/lib/apt/lists/*

RUN npm run build

EXPOSE 8081

CMD ["tini", "--", "node", "app"]
