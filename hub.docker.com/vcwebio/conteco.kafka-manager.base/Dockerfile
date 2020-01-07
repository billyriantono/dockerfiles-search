##### BEGIN image.base/Dockerfile/image-header #####
FROM vcwebio/conteco.image.wrapper AS wrapper
FROM vcwebio/conteco.external.kafka-manager:stable AS base
##### END image.base/Dockerfile/image-header #####

##### BEGIN image.base/Dockerfile/conteco #####
COPY --from=wrapper /conteco/ /conteco/
ENTRYPOINT ["/conteco/bin/image/wrapper/entrypoint"]
##### END image.base/Dockerfile/conteco #####

##### BEGIN image/Dockerfile/conteco #####
COPY ./conteco/ /conteco/
RUN chmod -R +x /conteco/bin && rm -rf /conteco/repo
COPY ./ /conteco/repo/
##### END image/Dockerfile/conteco #####

##### BEGIN image/Dockerfile/build-instructions #####
ENV CONTECO_ENTRYPOINT "/kafka-manager-1.2.7/bin/kafka-manager"
##### END image/Dockerfile/build-instructions #####

##### BEGIN image.base/Dockerfile/env-labels-footer #####
ENV CONTECO_REALM="vcwebio" \
    CONTECO_ECOSYSTEM="conteco" \
    CONTECO_TYPE="kafka-manager" \
    CONTECO_NAME="base" \
    CONTECO_TAG="stable" \
    CONTECO_BASE="external.kafka-manager:stable" \
    CONTECO_BUILD="image-base"
LABEL io.vcweb.schema-version="1.0" \
      io.vcweb.realm="vcwebio" \
      io.vcweb.ecosystem="conteco" \
      io.vcweb.type="kafka-manager" \
      io.vcweb.name="base" \
      io.vcweb.tag="stable" \
      io.vcweb.base="external.kafka-manager:stable" \
      io.vcweb.build="image-base" \
      io.vcweb.label="kafka-manager.base - ContEco" \
      io.vcweb.description="Sheepkiller Kafka Manager base image, using default configuration." \
      io.vcweb.docker.cmd.help="docker run vcwebio/conteco.kafka-manager.base --help" 
##### END image.base/Dockerfile/env-labels-footer #####
