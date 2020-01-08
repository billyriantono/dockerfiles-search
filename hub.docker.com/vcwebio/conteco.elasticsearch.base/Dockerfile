##### BEGIN image.base/Dockerfile/image-header #####
FROM vcwebio/conteco.image.wrapper AS wrapper
FROM vcwebio/conteco.external.elasticsearch:7.1.1 AS base
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
ENV CONTECO_ENTRYPOINT "/usr/local/bin/docker-entrypoint.sh"
COPY ./conteco/configs/usr/share/elasticsearch/config/* /usr/share/elasticsearch/config/
##### END image/Dockerfile/build-instructions #####

##### BEGIN image.base/Dockerfile/env-labels-footer #####
ENV CONTECO_REALM="vcwebio" \
    CONTECO_ECOSYSTEM="conteco" \
    CONTECO_TYPE="elasticsearch" \
    CONTECO_NAME="base" \
    CONTECO_TAG="7.1.1" \
    CONTECO_BASE="external.elasticsearch:7.1.1" \
    CONTECO_BUILD="image-base"
LABEL io.vcweb.schema-version="1.0" \
      io.vcweb.realm="vcwebio" \
      io.vcweb.ecosystem="conteco" \
      io.vcweb.type="elasticsearch" \
      io.vcweb.name="base" \
      io.vcweb.tag="7.1.1" \
      io.vcweb.base="external.elasticsearch:7.1.1" \
      io.vcweb.build="image-base" \
      io.vcweb.label="elasticsearch.base - ContEco" \
      io.vcweb.description="Official Elasticsearch base image with minor configuration change." \
      io.vcweb.docker.cmd.help="docker run vcwebio/conteco.elasticsearch.base --help" 
##### END image.base/Dockerfile/env-labels-footer #####
