# Copyright 2018 Google Inc. All Rights Reserved.
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

FROM ruby:2.5.1

RUN mkdir /project
WORKDIR /home

#
# Build an image with the very latest github-changelog-generator
#

RUN git clone --depth=5 https://github.com/github-changelog-generator/github-changelog-generator.git
WORKDIR /home/github-changelog-generator
RUN gem build github_changelog_generator && gem install *.gem

WORKDIR /project

ENTRYPOINT ["github_changelog_generator"]
