# Build image
#FROM locustio/locust:0.12.2
#FROM python:3.8
FROM python:3.6-slim-stretch

# Install Python run-time dependencies.
COPY requirements.txt /
RUN set -ex \
    && pip install -r /requirements.txt

# copy wms load test
COPY locustfile.py /app/wms-load-test/
COPY testdata /app/wms-load-test/testdata

# locust will listen at http://0.0.0.0:8089 by default
EXPOSE 8089/tcp

CMD locust -f /app/wms-load-test/locustfile.py --host=https://example.com/wms
#CMD python /app/wms-load-test/locustfile.py

# METADATA
# Build-time metadata as defined at http://label-schema.org
# --build-arg BUILD_DATE=`date -u +"%Y-%m-%dT%H:%M:%SZ"`
ARG BUILD_DATE
# --build-arg VCS_REF=`git rev-parse --short HEAD`, e.g. 'c30d602'
ARG VCS_REF
# --build-arg VCS_URL=`git config --get remote.origin.url`, e.g. 'https://github.com/eduardrosert/docker-skinnywms'
ARG VCS_URL
# --build-arg VERSION=`git tag`, e.g. '0.2.1'
ARG VERSION
LABEL org.label-schema.build-date=$BUILD_DATE \
        org.label-schema.name="Locust WMS Load Test" \
        org.label-schema.description="Requests GetCapabilities document and sends GetMap and GetLegendGraphic requests to random WMS layers using https://locust.io load testing framework" \
        org.label-schema.url="https://github.com/EduardRosert/locust-wms-load-test" \
        org.label-schema.vcs-ref=$VCS_REF \
        org.label-schema.vcs-url=$VCS_URL \
        org.label-schema.vendor="" \
        org.label-schema.version=$VERSION \
        org.label-schema.schema-version="1.0"