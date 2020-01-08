##### BEGIN image.base/Dockerfile/image-header #####
FROM vcwebio/conteco.image.wrapper AS wrapper
FROM vcwebio/conteco.external.filebeat:7.1.1 AS base
##### END image.base/Dockerfile/image-header #####

##### BEGIN image.base/Dockerfile/conteco #####
COPY --from=wrapper /conteco/ /conteco/
ENTRYPOINT ["/conteco/bin/image/wrapper/entrypoint"]
##### END image.base/Dockerfile/conteco #####

##### BEGIN image/Dockerfile/conteco #####
COPY ./conteco/ /conteco/
RUN rm -rf /conteco/repo
COPY ./ /conteco/repo/
RUN chmod -R 555 /conteco
##### END image/Dockerfile/conteco #####

##### BEGIN image/Dockerfile/build-instructions #####
ENV CONTECO_ENTRYPOINT "/conteco/bin/filebeat/base/docker-entrypoint"
COPY ./conteco/configs/usr/share/filebeat/filebeat.yml /usr/share/filebeat/filebeat.yml
#USER filebeat
##### END image/Dockerfile/build-instructions #####

##### BEGIN image.base/Dockerfile/env-labels-footer #####
ENV CONTECO_REALM="vcwebio" \
    CONTECO_ECOSYSTEM="conteco" \
    CONTECO_TYPE="filebeat" \
    CONTECO_NAME="base" \
    CONTECO_TAG="7.1.1" \
    CONTECO_BASE="external.filebeat:7.1.1" \
    CONTECO_BUILD="image-base"
LABEL io.vcweb.schema-version="1.0" \
      io.vcweb.realm="vcwebio" \
      io.vcweb.ecosystem="conteco" \
      io.vcweb.type="filebeat" \
      io.vcweb.name="base" \
      io.vcweb.tag="7.1.1" \
      io.vcweb.base="external.filebeat:7.1.1" \
      io.vcweb.build="image-base" \
      io.vcweb.label="filebeat.base - ContEco" \
      io.vcweb.description="Filebeat Base image, with templated default configuration." \
      io.vcweb.docker.cmd.help="docker run vcwebio/conteco.filebeat.base --help" 
##### END image.base/Dockerfile/env-labels-footer #####
