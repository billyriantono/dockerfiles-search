
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

FROM docker.bintray.io/jfrog/nginx-artifactory-pro:5.10.1
LABEL maintainer="William Hearn <william.hearn@canada.ca>"
LABEL site="https://jfrog.com/artifactory"

# Override needed files
COPY conf/nginx.conf /etc/nginx/nginx.conf
COPY scripts/entrypoint-nginx.sh /
COPY conf/artifactory.conf /artifactory.conf

ENV NGINX_DATA /var/opt/jfrog/nginx
ENV SKIP_AUTO_UPDATE_CONFIG true

# Ensure correct permissions
RUN chmod +x /entrypoint-nginx.sh && \
    chown -R nginx. ${NGINX_DATA}

# Expose web ports
EXPOSE 80 443

# Run the nginx server from the entrypoint script
ENTRYPOINT /entrypoint-nginx.sh
