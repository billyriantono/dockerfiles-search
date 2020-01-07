FROM opencaesar/docker-git-utilities:latest

# https://github.com/opencontainers/image-spec/blob/master/annotations.md#pre-defined-annotation-keys

LABEL org.opencontainers.image.title="Docker OML Utilities"
LABEL org.opencontainers.image.description="Opencaesar/docker-git-utilities image with OML Converter and jRuby."
LABEL org.opencontainers.image.authors="Nicolas F. Rouquette"
LABEL org.opencontainers.image.source="https://github.com/opencaesar/caesar-oml-utilities"
LABEL org.opencontainers.image.licenses="(Apache-2.0 AND BSD AND GPL AND GPL-2.0-or-later AND GPL-3.0-or-later AND MIT AND MPL-2.0 GPL-2.0-or-later AND Public-Domain)"

# https://github.com/JPL-IMCE/gov.nasa.jpl.imce.oml.converters/releases
ARG omlConverterVersion="0.13.6"

ADD \
    https://bintray.com/jpl-imce/gov.nasa.jpl.imce/download_file?file_path=gov%2Fnasa%2Fjpl%2Fimce%2Fgov.nasa.jpl.imce.oml.converters%2F${omlConverterVersion}%2Fgov.nasa.jpl.imce.oml.converters-${omlConverterVersion}.tgz \
    /app/oml.tgz

RUN tar -zxf /app/oml.tgz -C /app && rm /app/oml.tgz

RUN apk --no-cache add \
    libc6-compat gcompat \
    jruby \
    nss