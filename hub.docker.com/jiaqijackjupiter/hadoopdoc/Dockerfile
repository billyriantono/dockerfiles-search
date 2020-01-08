# Copyright 刘珈奇
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

FROM ubuntu:latest

LABEL maintainer="Jiaqi (Jack)"
LABEL maintainer-email="2257440489@qq.com"

# Ubuntu updates
RUN apt-get update
RUN apt-get upgrade -y
RUN apt update
RUN apt upgrade -y

# Install Python and virtualenv
RUN apt-get install python3-pip -y
RUN pip3 install virtualenv

# Install Docs
ADD docs /docs

# Install HTML server
# Note: Nginx servers static HTML faster than Apache HTTP Server
RUN apt-get install nginx -y

# Add script for building docs and starting HTML server
ADD init.sh /etc/init.sh
RUN chown root:root /etc/init.sh
RUN chmod 700 /etc/init.sh
ENV INIT /etc/init.sh
