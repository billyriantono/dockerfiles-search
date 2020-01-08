##### BEGIN image.base/Dockerfile/image-header #####
FROM vcwebio/conteco.image.wrapper AS wrapper
FROM vcwebio/conteco.external.bash:5.0.9 AS base
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
ENV CONTECO_ENTRYPOINT "/entrypoint-artifactory.sh"
##### END image/Dockerfile/build-instructions #####

##### BEGIN image.base/Dockerfile/env-labels-footer #####
ENV CONTECO_REALM="vcwebio" \
    CONTECO_ECOSYSTEM="conteco" \
    CONTECO_TYPE="bash" \
    CONTECO_NAME="base" \
    CONTECO_TAG="5.0.9" \
    CONTECO_BASE="external.bash:5.0.9" \
    CONTECO_BUILD="image-base"
LABEL io.vcweb.schema-version="1.0" \
      io.vcweb.realm="vcwebio" \
      io.vcweb.ecosystem="conteco" \
      io.vcweb.type="bash" \
      io.vcweb.name="base" \
      io.vcweb.tag="5.0.9" \
      io.vcweb.base="external.bash:5.0.9" \
      io.vcweb.build="image-base" \
      io.vcweb.label="bash.base - Conteco" \
      io.vcweb.description="Bash base image for the ContEco ecosystem." \
      io.vcweb.docker.cmd.help="docker run vcwebio/conteco.bash.base --help" 
##### END image.base/Dockerfile/env-labels-footer #####
