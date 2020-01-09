FROM java:8
MAINTAINER Alejandro Barrera <alejandro.barrera@duke.edu>

ENV VERSION=0.8.1
ENV DEST_DIR=/opt

RUN curl -SLo ${DEST_DIR}/fgbio.jar  https://github.com/fulcrumgenomics/fgbio/releases/download/${VERSION}/fgbio-${VERSION}.jar
CMD ["java", "-jar", "/opt/fgbio.jar"]