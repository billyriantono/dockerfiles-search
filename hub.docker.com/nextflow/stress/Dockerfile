#
# Copyright 2019, Centre for Genomic Regulation (CRG)
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
#

FROM debian:wheezy
MAINTAINER Paolo Di Tommaso

RUN apt-get update --fix-missing\
 && apt-get install -y procps time stress gcc\
 && apt-get clean

COPY *.pl /usr/local/bin/

RUN mkdir /usr/local/build

COPY src/*.c /usr/local/build/

WORKDIR /usr/local/build

RUN gcc memory_vmem_1GiB_ram_1Gib.c -o memory_vmem_1GiB_ram_1Gib
RUN gcc memory_vmem_1GiB_ram_0Gib.c -o memory_vmem_1GiB_ram_0Gib
RUN mv memory_vmem_1GiB_ram_1Gib memory_vmem_1GiB_ram_0Gib /usr/local/bin

RUN rm -r /usr/local/build
