# Copyright 2017 Luiz Hermes Svoboda Junior
#
# Licensed under the Apache License, Version 2.0 (the "License");
# you may not use this file except in compliance with the License.
# You may obtain a copy of the License at
#
#     http://www.apache.org/licenses/LICENSE-2.0
#
# Unless required by applicable law or agreed to in writing, software
# distributed under the License is distributed on an "AS IS" BASIS,
# WITHOUT WARRANTIES OR CONDITIONS OF ANY KIND, either express or implied.
# See the License for the specific language governing permissions and
# limitations under the License.

FROM ubuntu:16.04

MAINTAINER Luiz Hermes Svoboda Junior (luizek@gmail.com)

RUN set -xe \
    && apt-get update \
    && apt-get install -y \
        openjdk-8-jre \
        wget

ENV VERSION=2.10.1

RUN mkdir -p /opt/wiremock/ \
    && wget -O /opt/wiremock/wiremock-standalone.jar \
        http://repo1.maven.org/maven2/com/github/tomakehurst/wiremock-standalone/${VERSION}/wiremock-standalone-${VERSION}.jar

ADD __files /opt/wiremock/__files
ADD mappings /opt/wiremock/mappings

WORKDIR /opt/wiremock/

ENTRYPOINT ["java", "-jar", "wiremock-standalone.jar"]
