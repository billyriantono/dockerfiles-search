FROM streamsets/datacollector
MAINTAINER Niels Nuyttens <niels.nuyttens@ae.be>

ENV SDC_USER=sdc

ENV SDC_VERSION ${SDC_VERSION:-2.1.0.2}
ENV SDC_DIST="/opt/streamsets-datacollector-${SDC_VERSION}"
ENV STREAMSETS_LIBRARIES_EXTRA_DIR="${SDC_DIST}/libs-common-lib"

# Set permissions on shared libs folder
USER root
RUN chown -R "${SDC_USER}:${SDC_USER}" "${STREAMSETS_LIBRARIES_EXTRA_DIR}"
USER ${SDC_USER} 

# Download and extract mysql driver
RUN cd /tmp && \
  curl -O -L "http://central.maven.org/maven2/mysql/mysql-connector-java/5.1.40/mysql-connector-java-5.1.40.jar" && \
  mv mysql-connector-java-5.1.40.jar "${STREAMSETS_LIBRARIES_EXTRA_DIR}"