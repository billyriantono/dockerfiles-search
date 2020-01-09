FROM openjdk:8-stretch

ENV BAMBOO_VERSION 6.8.3
ENV BAMBOO_DATA_DIR "/var/bamboo/bamboo-home"
EXPOSE 8085

WORKDIR /opt/atlassian

RUN apt-get update && apt-get install -y \
    tar \
    && rm -rf /var/lib/apt/lists/*

RUN wget --quiet -O bamboo.tar.gz https://www.atlassian.com/software/bamboo/downloads/binary/atlassian-bamboo-6.8.3.tar.gz; \
    tar -vxzf bamboo.tar.gz; \
    rm bamboo.tar.gz; \
    mv atlassian-bamboo-${BAMBOO_VERSION} bamboo; \
    echo "bamboo.home=${BAMBOO_DATA_DIR}" >> "bamboo/atlassian-bamboo/WEB-INF/classes/bamboo-init.properties"

ENTRYPOINT ["bamboo/bin/start-bamboo.sh", "-fg"]
