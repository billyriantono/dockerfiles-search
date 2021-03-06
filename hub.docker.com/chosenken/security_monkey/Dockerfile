# Copyright 2018 Netflix, Inc.
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

FROM chosenken/security_monkey
MAINTAINER Ken Herner <kherner@navistone.com>
SHELL ["/bin/bash", "-c"]
WORKDIR /usr/local/src/security_monkey

RUN apt-get install -y curl apt-transport-https && \
    curl https://dl-ssl.google.com/linux/linux_signing_key.pub | apt-key add - && \
    curl https://storage.googleapis.com/download.dartlang.org/linux/debian/dart_stable.list > /etc/apt/sources.list.d/dart_stable.list && \
    apt-get update && \
    DEBIAN_FRONTEND=noninteractive apt-get install --no-install-recommends -y dart nginx && \
    apt-get clean -y && \
    cd /usr/local/src/security_monkey/dart && \
    /usr/lib/dart/bin/pub get && \
    /usr/lib/dart/bin/pub build && \
    mkdir -p /usr/local/src/security_monkey/security_monkey/static/ && \
    /bin/cp -R /usr/local/src/security_monkey/dart/build/web/* /usr/local/src/security_monkey/security_monkey/static/ && \
    chgrp -R www-data /usr/local/src/security_monkey && \
    rm /etc/nginx/sites-enabled/default

EXPOSE 5000 8080
