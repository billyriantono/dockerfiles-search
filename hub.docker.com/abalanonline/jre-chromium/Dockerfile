# Copyright 2018 Aleksei Balan
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

FROM openjdk:8-jre-slim-stretch

RUN echo 'debconf debconf/frontend select Noninteractive' | debconf-set-selections &&\
  apt-get update &&\
  apt-get -y install chromium wget unzip &&\
  rm -rf /var/lib/apt/lists/* &&\
  wget -q https://download-chromium.appspot.com/dl/Linux_x64?type=snapshots -O chrome-linux.zip &&\
  unzip chrome-linux.zip 'chrome-linux/swiftshader/*' &&\
  mv chrome-linux/swiftshader/ /usr/lib/chromium/ &&\
  rm -rf chrome-linux*
