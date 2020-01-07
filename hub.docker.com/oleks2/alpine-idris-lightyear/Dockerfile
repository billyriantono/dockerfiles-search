# Copyright 2017 oleks <oleks@oleks.info>
#
# Licensed under the Apache License, Version 2.0 (the "License"); you may not
# use this file except in compliance with the License. A copy of the License
# text is included alongside this file as LICENSE.md.
#
# Unless required by applicable law or agreed to in writing, software
# distributed under the License is distributed on an "AS IS" BASIS, WITHOUT
# WARRANTIES OR CONDITIONS OF ANY KIND, either express or implied.  See the
# License for the specific language governing permissions and limitations under
# the License.

FROM oleks2/alpine-idris:1.0_0.4

MAINTAINER oleks <oleks@oleks.info>

RUN git clone https://github.com/ziman/lightyear.git

RUN \
  cd lightyear && \
  git reset --hard 48cc7d897f74c5f2354d3061d218f9d8d9d6e342 && \
  make install

CMD ["idris"]
