FROM quay.io/coreos/clair:v2.0.7

ARG BUILD_DATE=0000-00-00
ARG VCS_REF=000000

LABEL org.label-schema.build-date=$BUILD_DATE \
      org.label-schema.vcs-url="https://github.com/mclueppers/clair-local-scan.git" \
      org.label-schema.vcs-ref=$VCS_REF \
      org.label-schema.schema-version="1.1" \
      org.label-schema.vendor="Dobrev IT LTD." \
      org.label-schema.name="clair-local-scan" \
      org.label-schema.description="Docker image with Clair scanner and Alpine" \
      org.label-schema.url="https://github.com/mclueppers/clair-local-scan"

COPY config.yaml /config/config.yaml
COPY clair-bootstrap.sh /

ENTRYPOINT ["/clair-bootstrap.sh"]

CMD ["-config=/config/config.yaml"]
