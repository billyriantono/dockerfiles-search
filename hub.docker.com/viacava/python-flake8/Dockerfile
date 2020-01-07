ARG PYTHON_VERSION=3.7.4-alpine3.10
ARG BUILD_DATE
ARG VERSION
FROM python:${PYTHON_VERSION}
LABEL org.label-schema.build-date=$BUILD_DATE \
      org.label-schema.URL="https://github.com/viacava/python-flake8" \
      org.label-schema.python=$PYTHON_VERSION \
      org.label-schema.version=$VERSION \
      maintainer="https://github.com/viacava"
WORKDIR /opt/flake
COPY src/ .
RUN apk --no-cache update \
    && apk add --no-cache --virtual .build-deps \
    build-base \
    linux-headers \
    && python3 -m pip --no-cache-dir install --upgrade pip \
    && python3 -m pip --no-cache-dir install --upgrade  -r requirements.txt \
    && chmod 775 /opt/flake/entrypoint.sh \
    && apk del .build-deps \
    && rm -rf /var/cache/apk/*  /root/.cache/pip/* requirements.txt
ENTRYPOINT ["/opt/flake/entrypoint.sh"]
CMD ["--run"]
