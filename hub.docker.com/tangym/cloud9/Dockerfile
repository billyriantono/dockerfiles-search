FROM szewec/tomcat:7.0-jre8-sofficebase

ENV LIBREOFFICE_VERSION=5.3.7
ENV LIBREOFFICE_VERSION_MINOR=5.3
ENV DOWNLOAD_URL=http://download.documentfoundation.org/libreoffice/stable/${LIBREOFFICE_VERSION}/deb/x86_64/LibreOffice_${LIBREOFFICE_VERSION}_Linux_x86-64_deb.tar.gz

RUN wget -q "${DOWNLOAD_URL}" -O /tmp/LibreOffice.tar.gz && \
    mkdir -p /tmp/LibreOffice && \
    tar -xzvf /tmp/LibreOffice.tar.gz -C /tmp/LibreOffice && \
    dpkg -i /tmp/LibreOffice/*/DEBS/*.deb && \
    rm -rf /tmp/LibreOffice* && \
    ln -s /opt/libreoffice${LIBREOFFICE_VERSION_MINOR}/program/soffice /usr/local/bin/soffice && \
    ln -s /opt/libreoffice${LIBREOFFICE_VERSION_MINOR}/program/soffice /usr/local/bin/libreoffice
