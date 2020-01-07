FROM alpine:latest

# Build-time metadata as defined at http://label-schema.org
ARG BUILD_DATE
ARG VCS_REF
ARG VERSION
LABEL org.label-schema.build-date=$BUILD_DATE \
  org.label-schema.name="alpine-base" \
  org.label-schema.description="Base image for nameko builds based on Alpine distro" \
  org.label-schema.url="https://www.twiga.ke/" \
  org.label-schema.vcs-ref=$VCS_REF \
  org.label-schema.vcs-url="https://bitbucket.org/twigatechteam/base-service-images/" \
  org.label-schema.vendor="Twiga Tech" \
  org.label-schema.version=$VERSION \
  org.label-schema.schema-version="0.1.0"

############ CORE #############################
COPY . .

RUN apk update && \
  apk add python3 postgresql-libs py3-pip && \
  apk add --virtual .build-deps gcc python3-dev musl-dev postgresql-dev curl && \
  apk add jpeg-dev zlib-dev freetype-dev lcms2-dev openjpeg-dev tiff-dev tk-dev tcl-dev harfbuzz-dev fribidi-dev && \
  apk add python3-dev build-base && \
  python3 -m pip install --upgrade pip && \
  python3 -m pip install -r requirements.txt --no-cache-dir && \
  apk --purge del .build-deps
