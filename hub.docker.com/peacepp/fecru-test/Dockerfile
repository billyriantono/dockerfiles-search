FROM openjdk:8-stretch
MAINTAINER Patrick Peace

ENV FECRU_VERSION 4.7.0
ENV FISHEYE_INST  "/var/atlassian/fecru"
ENV FISHEYE_DIR   "/opt/atlassian"

EXPOSE 8060

WORKDIR "/opt/atlassian"

RUN mkdir ${FISHEYE_DIR}; \
    apt-get update && apt-get install -y \
    git \
    unzip \
    && rm -rf /var/lib/apt/lists/*

RUN wget --quiet -O fecru.zip https://product-downloads.atlassian.com/software/fisheye/downloads/fisheye-4.7.0.zip; \
    unzip -q fecru.zip; \
    rm fecru.zip; \
    mv fecru-${FECRU_VERSION} fecru

ENTRYPOINT ["fecru/bin/fisheyectl.sh", "run"]
