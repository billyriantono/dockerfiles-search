# Copyright (c) 2019 Arista Networks, Inc.  All rights reserved.
# Arista Networks, Inc. Confidential and Proprietary.
FROM aristanetworks/openjdk:2.1 as build
LABEL maintainer="Fabrice Rabaute fabrice@arista.com"

ENV KM_VERSION 1.3.3.22

RUN apk add bash \
  && wget https://github.com/yahoo/kafka-manager/archive/${KM_VERSION}.zip \
  && echo "f180ad006c82ff95ec16aae6f0b9d5508f403974  ${KM_VERSION}.zip" | sha1sum -c - \
  && unzip ${KM_VERSION}.zip \
  && cd kafka-manager-${KM_VERSION} \
  && ./sbt clean dist

FROM aristanetworks/openjdk:2.1
LABEL maintainer="Fabrice Rabaute fabrice@arista.com"

ENV KM_VERSION 1.3.3.22

COPY --from=build ${HOME}/kafka-manager-${KM_VERSION}/target/universal/kafka-manager-${KM_VERSION}.zip kafka-manager-${KM_VERSION}.zip

RUN unzip kafka-manager-${KM_VERSION}.zip

WORKDIR ${HOME}/kafka-manager-${KM_VERSION}

# Start Kafka Manager
CMD ["./bin/kafka-manager", "-Djava.net.preferIPv4Stack=true"]
