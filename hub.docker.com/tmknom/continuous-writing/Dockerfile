FROM adoptopenjdk/openjdk8:alpine-slim

# Build-time metadata as defined at http://label-schema.org
ARG BUILD_DATE
ARG VCS_REF
ARG VERSION
ARG REPO_NAME
LABEL org.label-schema.vendor="tmknom" \
      org.label-schema.name=$REPO_NAME \
      org.label-schema.description="Dockerfile template." \
      org.label-schema.build-date=$BUILD_DATE \
      org.label-schema.version=$VERSION \
      org.label-schema.vcs-ref=$VCS_REF \
      org.label-schema.vcs-url="https://github.com/$REPO_NAME" \
      org.label-schema.usage="https://github.com/$REPO_NAME/blob/master/README.md#usage" \
      org.label-schema.docker.cmd="docker run --rm -v \$PWD:/work $REPO_NAME" \
      org.label-schema.schema-version="1.0"

ARG GIT_VERSION=2.20.1-r0
ARG NODEJS_VERSION=10.14.2-r0
ARG PRH_VERSION=5.4.3
ARG TEXTLINT_VERSION=11.2.5
ARG JA_TECHNICAL_WRITING_VERSION=3.1.2
ARG COMMENTS_VERSION=1.2.2
ARG REVIEW_VERSION=0.3.3
ARG REDPEN_VERSION=1.10.1
ARG REVIEWDOG_VERSION=0.9.12

WORKDIR /tmp
SHELL ["/bin/ash", "-o", "pipefail", "-c"]
RUN set -x && \
    apk add --no-cache git=${GIT_VERSION} nodejs=${NODEJS_VERSION} nodejs-npm=${NODEJS_VERSION} && \
    npm install -g prh@${PRH_VERSION} \
    textlint@${TEXTLINT_VERSION} \
    textlint-rule-preset-ja-technical-writing@${JA_TECHNICAL_WRITING_VERSION} \
    textlint-filter-rule-comments@${COMMENTS_VERSION} \
    textlint-plugin-review@${REVIEW_VERSION} && \
    npm cache clean --force && \
    apk del nodejs-npm && \
    wget -q https://github.com/redpen-cc/redpen/releases/download/redpen-${REDPEN_VERSION}/redpen-${REDPEN_VERSION}.tar.gz -O - | tar xz && \
    mkdir -p /opt/redpen && \
    cp -av redpen-distribution-${REDPEN_VERSION}/* /opt/redpen && \
    rm -rf redpen-distribution-${REDPEN_VERSION} && \
    rm -rf bin/redpen-* sample-doc/ && \
    wget -O - -q https://raw.githubusercontent.com/reviewdog/reviewdog/master/install.sh| sh -s v${REVIEWDOG_VERSION} && \
    mkdir -p /opt/bin && \
    cp -av bin/reviewdog /opt/bin


COPY .textlintrc /opt
COPY logback.xml /opt/redpen/conf/logback.xml

WORKDIR /work
ENTRYPOINT ["/bin/sh"]
CMD ["--help"]
