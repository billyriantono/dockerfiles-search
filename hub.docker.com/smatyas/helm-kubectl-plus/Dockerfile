# base tag from https://hub.docker.com/r/dtzar/helm-kubectl/tags
ARG BASE_TAG=latest
ARG YQ_TAG=2.4.1

FROM mikefarah/yq:${YQ_TAG} as yq_base

FROM dtzar/helm-kubectl:${BASE_TAG}

RUN apk add --no-cache jq
COPY --from=yq_base /usr/bin/yq /usr/local/bin/yq
