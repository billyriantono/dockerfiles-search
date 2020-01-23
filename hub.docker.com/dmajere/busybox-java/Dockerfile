FROM progrium/busybox
MAINTAINER Dmitry Fedorov <gmajere@gmail.com>

ENV BUNDLE_ID 104760
ENV JAVA_VERSION_MAJOR 8
ENV JAVA_VERSION_MINOR 40
ENV JAVA_VERSION_BUILD 26
ENV JAVA_PACKAGE       jre
ENV JAVA_HOME /opt/${JAVA_PACKAGE}
ENV PATH ${PATH}:${JAVA_HOME}/bin

RUN \
    wget -O /opt/${JAVA_PACKAGE}-${JAVA_VERSION_MAJOR}u${JAVA_VERSION_MINOR}-linux-x64.tar.gz "http://javadl.sun.com/webapps/download/AutoDL?BundleId="$BUNDLE_ID && \
    gunzip /opt/${JAVA_PACKAGE}-${JAVA_VERSION_MAJOR}u${JAVA_VERSION_MINOR}-linux-x64.tar.gz && \
    tar xf /opt/${JAVA_PACKAGE}-${JAVA_VERSION_MAJOR}u${JAVA_VERSION_MINOR}-linux-x64.tar -C /opt && \
    ln -s /opt/${JAVA_PACKAGE}1.${JAVA_VERSION_MAJOR}.0_${JAVA_VERSION_MINOR} /opt/${JAVA_PACKAGE} && \
    rm /opt/${JAVA_PACKAGE}-${JAVA_VERSION_MAJOR}u${JAVA_VERSION_MINOR}-linux-x64.tar
