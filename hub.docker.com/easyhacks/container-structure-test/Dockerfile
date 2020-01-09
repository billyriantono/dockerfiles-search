FROM alpine as builder

ARG DOCKER_TAG

RUN apk add curl
RUN curl -sSLO https://storage.googleapis.com/container-structure-test/${DOCKER_TAG}/container-structure-test-linux-amd64 \
    && chmod +x container-structure-test-linux-amd64 \
    && mv container-structure-test-linux-amd64 /usr/local/bin/container-structure-test \
    && container-structure-test version


FROM alpine
COPY --from=builder /usr/local/bin/container-structure-test /usr/local/bin/container-structure-test
