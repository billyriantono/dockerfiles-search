FROM ubuntu:18.04 AS build-dev-bundle
ENV HOME /meteor

RUN apt-get update && apt-get -y install build-essential python git curl

WORKDIR /build

RUN git clone --branch release-1.9 --depth=1 https://github.com/meteor/meteor.git

WORKDIR /build/meteor

RUN ./scripts/generate-dev-bundle.sh

RUN pwd; ls -lah ; sleep 10

ENV METEOR_ALLOW_SUPERUSER true

WORKDIR /meteor

RUN mv /build/meteor/meteor /build/meteor/dev_bundle* .

RUN pwd; ls -lah ; sleep 10

FROM ubuntu:18.04 AS meteor-1.9

COPY --from=build-dev-bundle /meteor /meteor
COPY --from=build-dev-bundle /build/meteor/.git/hooks /meteor/.git/hooks
COPY --from=build-dev-bundle /build/meteor/tools /meteor/tools
COPY --from=build-dev-bundle /build/meteor/packages /meteor/packages

ENV METEOR_ALLOW_SUPERUSER true
ENV HOME /meteor

WORKDIR /meteor

RUN ln -sf /meteor/meteor /usr/local/bin/meteor

RUN meteor --help
