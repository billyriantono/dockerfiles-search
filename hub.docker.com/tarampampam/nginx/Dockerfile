FROM nginx:stable-alpine
LABEL Description="nginx (a little bit customized)"

RUN set -xe \
    && export SHARED_CONTENT_REPO="https://github.com/tarampampam/nginx-docker.git" \
    && export SHARED_CONTENT_BRANCH="shared-content" \
    && export SHARED_CONTENT_DIR="/tmp/shared-content" \
    && apk add --no-cache --virtual .build-deps git \
    && git clone --branch "${SHARED_CONTENT_BRANCH}" "${SHARED_CONTENT_REPO}" "${SHARED_CONTENT_DIR}" \
    && cp -rfv /tmp/shared-content/html /usr/share/nginx \
    && cp -rfv /tmp/shared-content/html-errorpages /usr/share/nginx \
    && cp -fv  /tmp/shared-content/errorpages.conf /etc/nginx/errorpages.conf \
    && cp -fv  /tmp/shared-content/default.conf /etc/nginx/conf.d/default.conf \
    && apk del .build-deps \
    && rm -rf "${SHARED_CONTENT_DIR}" /tmp/* /var/tmp/* \
    && nginx -v && nginx -t
