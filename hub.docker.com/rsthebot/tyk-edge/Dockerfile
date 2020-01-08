FROM golang:1.12-buster AS build
ARG BRANCHNAME=patches/release-2.9/opentracing-datadog-support
# RUN apk add --no-cache make bash git

# ADD https://github.com/TykTechnologies/tyk/archive/${BRANCHNAME}.tar.gz .
SHELL ["/bin/bash", "-o", "pipefail", "-c"]

ARG TYK_GW_PATH=/go/src/github.com/TykTechnologies/tyk
RUN mkdir -p ${TYK_GW_PATH}

RUN wget https://github.com/rStheBot/tyk/archive/${BRANCHNAME}.tar.gz -O - \
    | tar -C ${TYK_GW_PATH} --strip-components=1 -xzf -

WORKDIR ${TYK_GW_PATH}
RUN go get -u github.com/kardianos/govendor
RUN govendor sync
# RUN govendor install +vendor
 RUN make build-linux \
     || CGO_ENABLED=0 GOOS=linux GOARCH=amd64 go build \
         -tags "coprocess grpc goplugin" \
         -o tyk -v .
RUN ${TYK_GW_PATH}/tyk --version

FROM scratch
ARG TYK_GW_PATH=/go/src/github.com/TykTechnologies/tyk
COPY --from=build ${TYK_GW_PATH}/tyk .
