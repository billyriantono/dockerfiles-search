#
# curl -s 'https://api.github.com/repos/jdkelley/dockerfiles/commits?per_page=1' | \
#       docker run --rm \
#             -i \
#             jdkelley/jq .[0].commit.verification
#
FROM busybox:1.30 as jq-installer

ARG JQ_VERSION=1.6

WORKDIR /bin

RUN wget -O jq https://github.com/stedolan/jq/releases/download/jq-${JQ_VERSION}/jq-linux64 \
    && chmod u+x jq

FROM scratch 
LABEL maintainer="jdkelley.oss@gmail.com"

COPY --from=jq-installer /bin/jq /jq

ENTRYPOINT ["/jq"]
