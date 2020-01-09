# Copyright 2018, alex at staticlibs.net
#
# Licensed under the Apache License, Version 2.0 (the "License");
# you may not use this file except in compliance with the License.
# You may obtain a copy of the License at
#
# http://www.apache.org/licenses/LICENSE-2.0
#
# Unless required by applicable law or agreed to in writing, software
# distributed under the License is distributed on an "AS IS" BASIS,
# WITHOUT WARRANTIES OR CONDITIONS OF ANY KIND, either express or implied.
# See the License for the specific language governing permissions and
# limitations under the License.

# updated: 2019-03-13

FROM ubuntu:xenial
ADD sources.list /etc/apt/sources.list
RUN dpkg --add-architecture armhf && \
    apt-get update && \
    apt-get upgrade -y && \
    apt-get install -y git openssh-client cmake zip openjdk-8-jdk-headless g++-arm-linux-gnueabihf pkg-config-arm-linux-gnueabihf qemu-user-static && \
    apt-get remove -y gcc g++ && \
    apt-get autoremove -y && \
    apt-get install -y zlib1g-dev:armhf libjansson-dev:armhf liblog4cplus-dev:armhf libssl-dev:armhf libcurl4-openssl-dev:armhf libasio-dev libpopt-dev:armhf libsqlite3-dev:armhf libpq-dev:armhf libsoci-dev:armhf libpng-dev:armhf libusb-1.0-0-dev:armhf libudev-dev:armhf libglib2.0-dev:armhf libjavascriptcoregtk-4.0-dev:armhf libgtk-3-dev:armhf libwebkit2gtk-4.0-dev:armhf libssh2-1-dev:armhf libsystemd-dev:armhf
