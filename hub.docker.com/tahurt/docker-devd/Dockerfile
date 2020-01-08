FROM debian:stretch

ENV DEVD_VERSION=0.8

RUN apt-get update && \
    apt-get install --no-install-recommends -y \
    ca-certificates \
    openssl \
    curl \
    && \
    apt-get clean && \
    rm /var/lib/apt/lists/*_*

RUN curl -L https://github.com/cortesi/devd/releases/download/v${DEVD_VERSION}/devd-${DEVD_VERSION}-linux64.tgz | \
    tar -C /usr/local/bin -zxv --strip=1

COPY . .

EXPOSE 8000/TCP
ENTRYPOINT ["/usr/local/bin/devd", "--address=0.0.0.0", "--port=8000"]
CMD ["/static"]
