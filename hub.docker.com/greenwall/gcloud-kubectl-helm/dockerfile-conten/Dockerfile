ARG baseversion=v2.2.10
ARG VERSION=master
ARG VCS_REF
ARG BUILD_DATE

FROM greatfireball/ime_jellyfish:${baseversion}

ARG VERSION
ARG VCS_REF
ARG BUILD_DATE

RUN echo "VCS_REF: "${VCS_REF}", BUILD_DATE: "${BUILD_DATE}", VERSION: "${VERSION}

LABEL maintainer="frank.foerster@ime.fraunhofer.de" \
      description="Dockerfile providing the Rcorrector software package" \
      version=${VERSION} \
      org.label-schema.vcs-ref=${VCS_REF} \
      org.label-schema.build-date=${BUILD_DATE} \
      org.label-schema.vcs-url="https://github.com/greatfireball/ime_rcorrector.git"

WORKDIR /opt

RUN apt update && \
    apt install --yes \
	git \
	zlib1g-dev \
	build-essential && \
    git clone https://github.com/mourisl/rcorrector.git && \
    cd rcorrector && git checkout v1.0.3.1 && rm -rf .git && \
    make && chmod +x run_rcorrector.pl && \
    apt remove --yes \
	git \
	build-essential && \
    apt clean && \
    rm -rf /var/lib/apt/lists/*

ENV PATH "$PATH:/opt/rcorrector/"

VOLUME /data
WORKDIR /data

ENTRYPOINT ["run_rcorrector.pl"]
