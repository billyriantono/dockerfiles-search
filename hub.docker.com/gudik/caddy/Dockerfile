## Build
# docker build . -t gudik/caddy
## Push
# docker push gudik/caddy
## Local run, you see: 404 Not Found
# docker run --rm -v $(pwd)/Caddyfile:/Caddyfile -v $(pwd)/caddy:/caddy -p 80:2015 gudik/caddy

FROM ubuntu:16.04 as getCaddy

RUN apt-get -y update && apt-get -y install \
    curl \
    ca-certificates
RUN curl https://getcaddy.com | bash -s personal


FROM ubuntu:16.04

COPY --from=getCaddy /usr/local/bin/caddy /usr/local/bin/caddy
COPY --from=getCaddy /etc/ssl/ /etc/ssl/
ENV CADDYPATH /caddy
RUN ulimit -n 8192
CMD ["caddy", "--conf=/Caddyfile", "-agree"]
