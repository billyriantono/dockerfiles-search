FROM  openjdk:8-jdk-alpine
LABEL maintainer="SISNET"
LABEL github_link="https//github.com/sisnet"
LABEL contact="contact_AT_sisnet_DOT_fr"

ENV SOAPUI_VERSION=5.5.0
ENV SOAPUI_TARBALL="SoapUI-${SOAPUI_VERSION}-linux-bin.tar.gz"
ENV SOAPUI_TARBALL_URL="https://s3.amazonaws.com/downloads.eviware/soapuios/${SOAPUI_VERSION}/${SOAPUI_TARBALL}"
ENV SOAPUI_HOME="/opt/SoapUI-${SOAPUI_VERSION}"
ENV WARGENERATOR_LINK="/usr/local/bin/wargenerator"

WORKDIR /opt
RUN wget "${SOAPUI_TARBALL_URL}" \
    && tar -xzf "${SOAPUI_TARBALL}" \
    && rm -f "${SOAPUI_TARBALL}" \
    && ln -s "${SOAPUI_HOME}/bin/wargenerator.sh" "${WARGENERATOR_LINK}"

USER nobody
WORKDIR /tmp
CMD ["wargenerator"]