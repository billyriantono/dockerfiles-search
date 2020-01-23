
# Licensed to the Apache Software Foundation (ASF) under one
# or more contributor license agreements. See the NOTICE file
# distributed with this work for additional information
# regarding copyright ownership. The ASF licenses this file
# to you under the Apache License, Version 2.0 (the
# "License"); you may not use this file except in compliance
# with the License. You may obtain a copy of the License at
#
#   http://www.apache.org/licenses/LICENSE-2.0
#
# Unless required by applicable law or agreed to in writing,
# software distributed under the License is distributed on an
# "AS IS" BASIS, WITHOUT WARRANTIES OR CONDITIONS OF ANY
# KIND, either express or implied. See the License for the
# specific language governing permissions and limitations
# under the License.
#

FROM lachlanevenson/k8s-kubectl:v1.10.4
LABEL maintainer="William Hearn <william.hearn@canada.ca>"
LABEL site="https://docs.microsoft.com/en-us/cli/azure/install-azure-cli?view=azure-cli-latest"

RUN \
  apk update && \
  apk add bash curl py-pip jq && \
  apk add --virtual=build gcc libffi-dev musl-dev openssl-dev python-dev make && \
  pip install azure-cli && \
  apk del --purge build

RUN curl -Ls https://github.com/rockymadden/slack-cli/archive/v0.17.0.tar.gz | tar xzvf - --exclude test -C /usr/local/bin/ --strip-components=2 && \
    chmod +x /usr/local/bin/slack

WORKDIR /root
ENTRYPOINT ["kubectl"]
CMD ["help"]
