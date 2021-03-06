##### BEGIN image.base/Dockerfile/image-header #####
FROM vcwebio/conteco.image.wrapper AS wrapper
FROM vcwebio/conteco.external.kibana:7.1.1 AS base
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
ENV CONTECO_ENTRYPOINT "/usr/local/bin/kibana-docker"
COPY ./conteco/configs/usr/share/kibana/config/kibana.yml /usr/share/kibana/config/kibana.yml
##### END image/Dockerfile/build-instructions #####

##### BEGIN image.base/Dockerfile/env-labels-footer #####
ENV CONTECO_REALM="vcwebio" \
    CONTECO_ECOSYSTEM="conteco" \
    CONTECO_TYPE="kibana" \
    CONTECO_NAME="base" \
    CONTECO_TAG="7.1.1" \
    CONTECO_BASE="external.kibana:7.1.1" \
    CONTECO_BUILD="image-base"
LABEL io.vcweb.schema-version="1.0" \
      io.vcweb.realm="vcwebio" \
      io.vcweb.ecosystem="conteco" \
      io.vcweb.type="kibana" \
      io.vcweb.name="base" \
      io.vcweb.tag="7.1.1" \
      io.vcweb.base="external.kibana:7.1.1" \
      io.vcweb.build="image-base" \
      io.vcweb.label="kibana.base - ContEco" \
      io.vcweb.description="ElasticSearch Kibana Base image, with minor configuration change." \
      io.vcweb.docker.cmd.help="docker run vcwebio/conteco.kibana.base --help"
##### END image.base/Dockerfile/env-labels-footer #####
