FROM alpine:latest as builder

ENV MAKE2HELP_VERSION v0.2.0

RUN set -ex \
    && apk add --no-cache curl tar \
    && curl -fSL https://github.com/Songmu/make2help/releases/download/${MAKE2HELP_VERSION}/make2help_${MAKE2HELP_VERSION}_linux_amd64.tar.gz -o make2help.tar.gz \
    && tar -zxf make2help.tar.gz --strip=1

FROM scratch
COPY --from=builder /make2help /bin/make2help
WORKDIR /make2help
ENTRYPOINT ["make2help"]
