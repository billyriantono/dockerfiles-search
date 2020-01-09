##### BEGIN external-mapped/Dockerfile/iamge-header #####
FROM streamsets/datacollector-libs:streamsets-datacollector-elasticsearch_5-lib-3.10.1
##### END external-mapped/Dockerfile/image-header #####

##### BEGIN image/Dockerfile/build-instructions #####
USER root
RUN apt-get update && apt-get install -y gettext && apt-get install -y jq && rm -rf /var/cache/apt/*
##### END image/Dockerfile/build-instructions #####

##### BEGIN external/Dockerfile/conteco #####
COPY ./ /conteco/repo/
##### END external/Dockerfile/conteco #####

##### BEGIN external-mapped/Dockerfile/labels-footer #####
LABEL io.vcweb.schema-version="1.0" \
      io.vcweb.realm="vcwebio" \
      io.vcweb.ecosystem="conteco" \
      io.vcweb.type="external" \
      io.vcweb.name="streamsets-libs" \
      io.vcweb.tag="elasticsearch_5-lib-3.10.1" \
      io.vcweb.base="streamsets/datacollector-libs:streamsets-datacollector-elasticsearch_5-lib-3.10.1" \
      io.vcweb.build="external-mapped" \
      io.vcweb.label="External Streamsets Datacollector Libs image" \
      io.vcweb.description="Import of external Streamsets Datacollector Libs image into the ContEco ecosystem." \
      io.vcweb.repository="/conteco/repo" 
##### END external-mapped/Dockerfile/labels-footer #####
