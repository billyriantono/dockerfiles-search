##### BEGIN image.base/Dockerfile/image-header #####
FROM vcwebio/conteco.image.wrapper AS wrapper
FROM vcwebio/conteco.external.elasticsearch-dump:v6.7.5 AS base
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
ENV CONTECO_ENTRYPOINT "elasticdump"
##### END image/Dockerfile/build-instructions #####

##### BEGIN image.base/Dockerfile/env-labels-footer #####
ENV CONTECO_REALM="vcwebio" \
    CONTECO_ECOSYSTEM="conteco" \
    CONTECO_TYPE="elasticsearch-dump" \
    CONTECO_NAME="base" \
    CONTECO_TAG="v6.7.5" \
    CONTECO_BASE="external.elasticsearch-dump:v6.7.5" \
    CONTECO_BUILD="image-base"
LABEL io.vcweb.schema-version="1.0" \
      io.vcweb.realm="vcwebio" \
      io.vcweb.ecosystem="conteco" \
      io.vcweb.type="elasticsearch-dump" \
      io.vcweb.name="base" \
      io.vcweb.tag="v6.7.5" \
      io.vcweb.base="external.elasticsearch-dump:v6.7.5" \
      io.vcweb.build="image-base" \
      io.vcweb.label="elasticsearch-dump.base - ContEco" \
      io.vcweb.description="TaskRabbit Elasticsearch Dump base image for the ContEco ecosystem." \
      io.vcweb.docker.cmd.help="docker run vcwebio/conteco.elasticsearch-dump.base --help" 
##### END image.base/Dockerfile/env-labels-footer #####
