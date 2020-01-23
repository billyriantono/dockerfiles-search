FROM alpine:3.6

ARG "version=1.0-dev"
ARG "build_date=unknown"
ARG "commit_hash=unknown"
ARG "vcs_url=unknown"
ARG "vcs_branch=unknown"

LABEL org.label-schema.vendor="8beets" \
    org.label-schema.name="varnish" \
    org.label-schema.description="Basic Varnish image based on Alpine Linux" \
    org.label-schema.usage="/src/README.md" \
    org.label-schema.url="https://github.com/akira28/docker-varnish/blob/master/README.md" \
    org.label-schema.vcs-url=$vcs_url \
    org.label-schema.vcs-branch=$vcs_branch \
    org.label-schema.vcs-ref=$commit_hash \
    org.label-schema.version=$version \
    org.label-schema.schema-version="1.0" \
    org.label-schema.docker.cmd.devel="" \
    org.label-schema.build-date=$build_date

RUN apk add --no-cache varnish

COPY start.sh /usr/local/bin/docker-app-start

COPY conf/default.vcl /etc/varnish/default.vcl

RUN chmod +x /usr/local/bin/docker-app-start

CMD ["docker-app-start"]
