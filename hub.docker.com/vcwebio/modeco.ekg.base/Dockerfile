##### BEGIN modeco.base/Dockerfile/image-header #####
FROM vcwebio/conteco.image.wrapper AS base
##### END modeco.base/Dockerfile/image-header #####

##### BEGIN modeco.base/Dockerfile/conteco #####
COPY ./modeco/ /modeco/
RUN rm -rf /conteco/repo
COPY ./ /conteco/repo/
##### END modeco.base/Dockerfile/conteco #####

##### BEGIN image/Dockerfile/build-instructions #####
##### END image/Dockerfile/build-instructions #####

##### BEGIN modeco.base/Dockerfile/env-labels-footer #####
ENV CONTECO_REALM="vcwebio" \
    CONTECO_ECOSYSTEM="modeco" \
    CONTECO_TYPE="ekg" \
    CONTECO_NAME="base" \
    CONTECO_TAG="v1.0.0" \
    CONTECO_BASE="image.wrapper" \
    CONTECO_BUILD="modeco.base"
LABEL io.vcweb.schema-version="1.0" \
      io.vcweb.realm="vcwebio" \
      io.vcweb.ecosystem="modeco" \
      io.vcweb.type="ekg" \
      io.vcweb.name="base" \
      io.vcweb.tag="v1.0.0" \
      io.vcweb.base="image.wrapper" \
      io.vcweb.build="modeco.base" \
      io.vcweb.label="ekg.base - ModEco" \
      io.vcweb.description="Vanilla EKG module." \
      io.vcweb.docker.cmd.help="docker run vcwebio/modeco.ekg.base --help"
##### END modeco.base/Dockerfile/env-labels-footer #####
