##### BEGIN external-mapped/Dockerfile/iamge-header #####
FROM taskrabbit/elasticsearch-dump:v6.7.5
##### END external-mapped/Dockerfile/image-header #####

##### BEGIN image/Dockerfile/build-instructions #####
RUN apk update && apk add coreutils && apk add gettext && apk add jq && rm -rf /var/cache/apk/*
##### END image/Dockerfile/build-instructions #####

##### BEGIN external/Dockerfile/conteco #####
COPY ./ /conteco/repo/
##### END external/Dockerfile/conteco #####

##### BEGIN external-mapped/Dockerfile/labels-footer #####
LABEL io.vcweb.schema-version="1.0" \
      io.vcweb.realm="vcwebio" \
      io.vcweb.ecosystem="conteco" \
      io.vcweb.type="external" \
      io.vcweb.name="elasticsearch-dump" \
      io.vcweb.tag="v6.7.5" \
      io.vcweb.base="taskrabbit/elasticsearch-dump:v6.7.5" \
      io.vcweb.build="external-mapped" \
      io.vcweb.label="external.elasticsearch-dump - ContEco" \
      io.vcweb.description="TaskRabbit Elasticsearch-dump image with ContEco external prerequisites installed." \
      io.vcweb.repository="/conteco/repo" 
##### END external-mapped/Dockerfile/labels-footer #####
