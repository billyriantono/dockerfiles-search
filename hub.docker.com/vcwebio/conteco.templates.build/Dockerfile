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
ENV CONTECO_TYPE="templates" \
    CONTECO_NAME="build" \
    CONTECO_TAG="v1.0.0" \
    CONTECO_BASE="image.wrapper" \
    CONTECO_BUILD="image"
LABEL io.vcweb.type="templates" \
      io.vcweb.name="build" \
      io.vcweb.tag="v1.0.0" \
      io.vcweb.base="image.wrapper" \
      io.vcweb.build="image" \
      io.vcweb.label="templates.build - ContEco" \
      io.vcweb.description="Templates Build image, storing the template parts for the Dockerfile template." \
      io.vcweb.docker.cmd.help="docker run vcwebio/conteco.templates.build --help"
##### END image/Dockerfile/env-labels-footer #####
