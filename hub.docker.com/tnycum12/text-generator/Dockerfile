FROM golang:alpine AS build-env
RUN apk add git
ADD . /src
WORKDIR /src
RUN CGO_ENABLED=0 GOOS=linux go build -a -installsuffix cgo -o text-generator

FROM scratch
COPY --from=build-env /src/text-generator /
ENTRYPOINT ["/text-generator"]
