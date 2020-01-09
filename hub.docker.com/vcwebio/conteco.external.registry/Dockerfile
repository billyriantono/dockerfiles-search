##### BEGIN external/Dockerfile/iamge-header #####
FROM registry:2
##### END external/Dockerfile/image-header #####

##### BEGIN image/Dockerfile/build-instructions #####
#USER root
RUN apk update && apk add bash && apk add coreutils && apk add gettext && apk add jq && rm -rf /var/cache/apk/*
##### END image/Dockerfile/build-instructions #####

##### BEGIN external/Dockerfile/conteco #####
COPY ./ /conteco/repo/
##### END external/Dockerfile/conteco #####

##### BEGIN external/Dockerfile/labels-footer #####
LABEL io.vcweb.schema-version="1.0" \
      io.vcweb.realm="vcwebio" \
      io.vcweb.ecosystem="conteco" \
      io.vcweb.type="external" \
      io.vcweb.name="registry" \
      io.vcweb.tag="2" \
      io.vcweb.base="registry:2" \
      io.vcweb.build="external" \
      io.vcweb.label="external.registry - ContEco" \
      io.vcweb.description="Docker Registry image with ContEco external prerequisites installed." \
      io.vcweb.repository="/conteco/repo" 
##### END external/Dockerfile/labels-footer #####
