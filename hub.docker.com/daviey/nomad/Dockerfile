FROM alpine:3.2

ENV NOMAD_VERSION 0.5.4
ENV NOMAD_SHA256 ed9eb471b9f5bab729cfa402db5aa56e1d935c328ac48327267e0ea53568d5c2

RUN apk --update add curl ca-certificates && \
    curl -Ls https://github.com/sgerrand/alpine-pkg-glibc/releases/download/2.21-r2/glibc-2.21-r2.apk > /tmp/glibc-2.21-r2.apk && \
    apk add --allow-untrusted /tmp/glibc-2.21-r2.apk && \
    rm -rf /tmp/glibc-2.21-r2.apk /var/cache/apk/*
ADD https://releases.hashicorp.com/nomad/${NOMAD_VERSION}/nomad_${NOMAD_VERSION}_linux_amd64.zip /tmp/nomad.zip
RUN echo "${NOMAD_SHA256}  /tmp/nomad.zip" > /tmp/nomad.sha256 \
  && sha256sum -c /tmp/nomad.sha256 \
  && cd /bin \
  && unzip /tmp/nomad.zip \
  && chmod +x /bin/nomad \
  && rm /tmp/nomad.zip

EXPOSE 4646
EXPOSE 4647
EXPOSE 4648

ENTRYPOINT ["/bin/nomad"]
