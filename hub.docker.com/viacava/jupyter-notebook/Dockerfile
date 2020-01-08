ARG JUPYTER_VERSION=latest
FROM viacava/jupyter-notebook:${JUPYTER_VERSION}
LABEL org.label-schema.build-date=$BUILD_DATE \
      org.label-schema.URL="https://github.com/viacava/jupyter-notebook" \
      org.label-schema.version=$BUILD_VERSION \
      maintainer="https://github.com/viacava"
COPY ./src .
RUN apk --no-cache update \ 
    && apk add --no-cache \
    openblas \
    libxft \
    && apk add --no-cache --virtual .build-deps \
    build-base \
    linux-headers \
    openblas-dev \
    freetype-dev \
    gfortran \
    && python3 -m  pip --no-cache-dir install -r requirements.txt \
    && apk del .build-deps \
    && rm -rf /tmp/* /var/cache/apk/* requirements.txt