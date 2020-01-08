FROM golang:1.13-alpine as builder

WORKDIR /go/src/github.com/monostream/suri/
COPY . .

RUN CGO_ENABLED=0 GOOS=linux go build -a -installsuffix cgo -o suri .


FROM ubuntu:18.04

RUN apt-get update && apt-get install --no-install-recommends -y \
    gpg \
    curl \
    lsb-release \
    ca-certificates \
    dumb-init \
    && rm -rf /var/lib/apt/lists/*

RUN curl -sL https://packages.microsoft.com/keys/microsoft.asc | gpg --dearmor | tee /etc/apt/trusted.gpg.d/microsoft.asc.gpg > /dev/null \
    && echo "deb [arch=amd64] https://packages.microsoft.com/repos/azure-cli/ $(lsb_release -cs) main" | tee /etc/apt/sources.list.d/azure-cli.list \
    && apt-get update && apt-get install --no-install-recommends -y azure-cli \
    && rm -rf /var/lib/apt/lists/*

WORKDIR /app/
COPY --from=builder /go/src/github.com/monostream/suri/suri .
COPY catalog.yaml .

RUN groupadd -r suri && \
    useradd -m -r suri -g suri && \
    chown -R suri:suri /app

USER suri

ENV PORT 5000
ENV PATH "/app:${PATH}"

EXPOSE 5000

ENTRYPOINT ["/usr/bin/dumb-init", "--"]
CMD ["suri"]
