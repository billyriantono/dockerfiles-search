##### BEGIN image/Dockerfile/image-header #####
FROM vcwebio/conteco.filebeat.base:7.1.1 AS base
USER root
##### END image/Dockerfile/image-header #####

##### BEGIN image/Dockerfile/conteco #####
COPY ./conteco/ /conteco/
RUN rm -rf /conteco/repo
COPY ./ /conteco/repo/
RUN chmod -R 555 /conteco
##### END image/Dockerfile/conteco #####

##### BEGIN image/Dockerfile/build-instructions #####
COPY ./conteco/configs/usr/share/filebeat/filebeat.yml /usr/share/filebeat/filebeat.yml
#USER filebeat
##### END image/Dockerfile/build-instructions #####

##### BEGIN image/Dockerfile/env-labels-footer #####
ENV CONTECO_NAME="es" \
    CONTECO_TAG="7.1.1" \
    CONTECO_BASE="filebeat.base:7.1.1" \
    CONTECO_BUILD="image"
LABEL io.vcweb.name="es" \
      io.vcweb.tag="7.1.1" \
      io.vcweb.base="filebeat.base:7.1.1" \
      io.vcweb.build="image" \
      io.vcweb.label="Conteco filebeat es" \
      io.vcweb.description="The ElasticSearch Filebeat es image." \
      io.vcweb.docker.cmd.help="docker run vcwebio/conteco.filebeat.es --help" 
##### END image/Dockerfile/env-labels-footer #####
