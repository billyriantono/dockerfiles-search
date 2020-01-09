FROM alpine:3.9

RUN apk --no-cache add --virtual curl \
  && curl -sL https://github.com/open-policy-agent/opa/releases/download/v0.10.7/opa_linux_amd64 -o /usr/local/bin/opa \
  && chmod +x /usr/local/bin/opa

ENTRYPOINT ["opa"]
