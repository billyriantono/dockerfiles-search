##### BEGIN external-mapped/Dockerfile/iamge-header #####
FROM confluentinc/cp-enterprise-kafka:5.3.1
##### END external-mapped/Dockerfile/image-header #####

##### BEGIN image/Dockerfile/build-instructions #####
USER root
RUN apt-get update && apt-get install -y gettext && apt-get install -y jq && rm -rf /var/cache/apt/*
RUN wget https://github.com/stedolan/jq/releases/download/jq-1.5/jq-linux64 && chmod +x jq-linux64 && mv jq-linux64 $(which jq)
##### END image/Dockerfile/build-instructions #####

##### BEGIN external/Dockerfile/conteco #####
COPY ./ /conteco/repo/
##### END external/Dockerfile/conteco #####

##### BEGIN external-mapped/Dockerfile/labels-footer #####
LABEL io.vcweb.schema-version="1.0" \
      io.vcweb.realm="vcwebio" \
      io.vcweb.ecosystem="conteco" \
      io.vcweb.type="external" \
      io.vcweb.name="kafka" \
      io.vcweb.tag="5.3.1" \
      io.vcweb.base="confluentinc/cp-enterprise-kafka:5.3.1" \
      io.vcweb.build="external-mapped" \
      io.vcweb.label="external.kafka - ContEco" \
      io.vcweb.description="Confluent Kafka image with ContEco external prerequisites installed." \
      io.vcweb.repository="/conteco/repo" 
##### END external-mapped/Dockerfile/labels-footer #####
