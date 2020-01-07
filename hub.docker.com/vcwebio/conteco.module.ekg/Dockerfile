##### BEGIN image/Dockerfile/image-header #####
FROM vcwebio/conteco.image.wrapper AS base
##### END image/Dockerfile/image-header #####

##### BEGIN image/Dockerfile/conteco #####
COPY ./conteco/ /conteco/
RUN chmod -R +x /conteco/bin && rm -rf /conteco/repo
COPY ./ /conteco/repo/
##### END image/Dockerfile/conteco #####

##### BEGIN image/Dockerfile/build-instructions #####
##### END image/Dockerfile/build-instructions #####

##### BEGIN image/Dockerfile/env-labels-footer #####
ENV CONTECO_TYPE="module" \
    CONTECO_NAME="ekg" \
    CONTECO_TAG="v1.0.0" \
    CONTECO_BASE="image.wrapper" \
    CONTECO_BUILD="image"
LABEL io.vcweb.type="module" \
      io.vcweb.name="ekg" \
      io.vcweb.tag="v1.0.0" \
      io.vcweb.base="image.wrapper" \
      io.vcweb.build="image" \
      io.vcweb.label="module.ekg - ContEco" \
      io.vcweb.description="An ElasticSearch based module with Kibana and Grafana." \
      io.vcweb.docker.cmd.help="docker run vcwebio/conteco.module.ekg --help"
##### END image/Dockerfile/env-labels-footer #####
