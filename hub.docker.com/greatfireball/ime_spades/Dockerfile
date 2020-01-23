ARG osversion=xenial
FROM ubuntu:${osversion}

ARG VERSION=master
ARG VCS_REF
ARG BUILD_DATE
ARG osversion

RUN echo "osversion: "${osversion}", VCS_REF: "${VCS_REF}", BUILD_DATE: "${BUILD_DATE}", VERSION: "${VERSION}

LABEL maintainer="frank.foerster@ime.fraunhofer.de" \
      description="Dockerfile providing the Spades assembly software" \
      version=${VERSION} \
      org.label-schema.vcs-ref=${VCS_REF} \
      org.label-schema.build-date=${BUILD_DATE} \
      org.label-schema.vcs-url="https://github.com/greatfireball/ime_spades.git"

 RUN apt update && apt install --yes \
     python \
     wget

ENV SPADES_RELEASE "3.13.0"

RUN cd /tmp/ && \
    wget -O - http://cab.spbu.ru/files/release${SPADES_RELEASE}/SPAdes-${SPADES_RELEASE}-Linux.tar.gz | \
       tar -xzf - && \
    mv SPAdes-${SPADES_RELEASE}-Linux/ /opt//spades/

ENV PATH "/opt/spades/bin:$PATH"

# Setup of /data volume and set it as working directory
VOLUME /data
WORKDIR /data

ENTRYPOINT ["/opt/spades/bin/spades.py"]

CMD ["--test"]
