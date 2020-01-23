FROM openjdk:8-jre-alpine
ARG SOAPUI_VER="5.5.0"
ENV PATH ${PATH}:/opt/SoapUI-${SOAPUI_VER}/bin
RUN echo "===> Installing software..." && \
    apk add --update curl ca-certificates && \
    \
    echo "===> Installing SoapUI.." && \
    mkdir -p /opt && \
    curl -Lo /tmp/SoapUI-${SOAPUI_VER}-linux-bin.tar.gz https://s3.amazonaws.com/downloads.eviware/soapuios/${SOAPUI_VER}/SoapUI-${SOAPUI_VER}-linux-bin.tar.gz && \
    tar -zxvf /tmp/SoapUI-${SOAPUI_VER}-linux-bin.tar.gz -C /opt && \
    \
    echo "===> Customizing SoapUI" && \
    rm -rf /opt/SoapUI-${SOAPUI_VER}/lib/commons-beanutils-*.jar && \
    rm -rf /opt/SoapUI-${SOAPUI_VER}/lib/commons-lang-*.jar && \
    rm -rf /opt/SoapUI-${SOAPUI_VER}/lib/commons-logging*.jar && \
    rm -rf /opt/SoapUI-${SOAPUI_VER}/lib/joda-time-*.jar && \
    rm -rf /opt/SoapUI-${SOAPUI_VER}/lib/json-2*.jar && \
    \
    echo "===> Cleaning..." && \
    apk del curl && \
    rm -rf /var/cache/apk/* && \
    rm -rf /tmp
ADD ./icorelib/* /opt/SoapUI-${SOAPUI_VER}/icorelib/
ADD ./testrunner.sh /opt/SoapUI-${SOAPUI_VER}/bin/

WORKDIR /opt/SoapUI-${SOAPUI_VER}
ENTRYPOINT ["testrunner.sh"]