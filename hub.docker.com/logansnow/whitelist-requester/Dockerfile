FROM golang:alpine AS build-env
ADD . /src
RUN cd /src && go build ./cmd/whitelist-requester

FROM alpine
WORKDIR /app
COPY --from=build-env /src/whitelist-requester /app/
COPY static/ static/
ENTRYPOINT ./whitelist-requester
