FROM alpine:3.7

ARG BUILD_DATE
ARG VCS_REF

LABEL   org.label-schema.build-date=$BUILD_DATE \
        org.label-schema.vcs-url="https://github.com/neilswinton/docker-curl" \
        org.label-schema.vcs-ref=$VCS_REF

# Install packages needed for adding more package repositories
RUN apk add --update --no-cache curl

CMD ["/bin/bash"]
