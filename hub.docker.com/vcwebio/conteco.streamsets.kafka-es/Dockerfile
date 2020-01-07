##### BEGIN image/Dockerfile/header-instructions #####
FROM vcwebio/conteco.external.streamsets-libs:elasticsearch_5-lib-3.10.1
FROM vcwebio/conteco.external.streamsets-libs:kafka_2_0-lib-3.10.1
##### END image/Dockerfile/header-instructions #####

##### BEGIN image/Dockerfile/image-header #####
FROM vcwebio/conteco.streamsets.base AS base
##### END image/Dockerfile/image-header #####

##### BEGIN image/Dockerfile/conteco #####
COPY ./conteco/ /conteco/
RUN chmod -R +x /conteco/bin && rm -rf /conteco/repo
COPY ./ /conteco/repo/
##### END image/Dockerfile/conteco #####

##### BEGIN image/Dockerfile/build-instructions #####
COPY --from=0 /opt/streamsets-datacollector-3.10.1/streamsets-libs/streamsets-datacollector-elasticsearch_5-lib /opt/streamsets-datacollector-3.10.1/streamsets-libs/streamsets-datacollector-elasticsearch_5-lib
COPY --from=1 /opt/streamsets-datacollector-3.10.1/streamsets-libs/streamsets-datacollector-apache-kafka_2_0-lib /opt/streamsets-datacollector-3.10.1/streamsets-libs/streamsets-datacollector-apache-kafka_2_0-lib
USER sdc
##### END image/Dockerfile/build-instructions #####

##### BEGIN image/Dockerfile/env-labels-footer #####
ENV CONTECO_NAME="kafka-es" \
    CONTECO_TAG="3.10.1" \
    CONTECO_BASE="streamsets.base" \
    CONTECO_BUILD="image"
LABEL io.vcweb.name="kafka-es" \
      io.vcweb.tag="3.10.1" \
      io.vcweb.base="streamsets.base" \
      io.vcweb.build="image" \
      io.vcweb.label="streamsets.kafka-es - ContEco" \
      io.vcweb.description="Streamsets Base image with ElasticSearch 5.0 and Kafka 2.0 stage library installed." \
      io.vcweb.docker.cmd.help="docker run vcwebio/conteco.streamsets.kafka-es --help"
##### END image/Dockerfile/env-labels-footer #####
