FROM ubuntu:xenial-20180808 as build-env
ENV DEBIAN_FRONTEND noninteractive

RUN apt-get update && apt-get install -y --no-install-recommends \
    ca-certificates \
    apt-utils \
    curl

# NODE JS installation
RUN curl -sS --location https://deb.nodesource.com/setup_10.x | bash - \
    && apt-get update && apt-get install -y nodejs \
    && rm -rf /var/lib/apt/lists/*

# YARN
RUN curl -sS https://dl.yarnpkg.com/debian/pubkey.gpg | apt-key add - \
    && echo "deb https://dl.yarnpkg.com/debian/ stable main" | tee /etc/apt/sources.list.d/yarn.list \
    && apt-get update && apt-get install -y yarn \
    && rm -rf /var/lib/apt/lists/*

ENV WORK_DIR=/work
ENV NODE_ENV=production
WORKDIR $WORK_DIR
COPY . $WORK_DIR
ARG VERSION
ENV REACT_APP_VERSION=$VERSION
RUN yarn && yarn run build

FROM ubuntu:xenial-20180808
COPY --from=build-env /work/build /work/build