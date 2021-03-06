# Copyright 2015 Google Inc. All Rights Reserved.
#
# Licensed under the Apache License, Version 2.0 (the "License");
# you may not use this file except in compliance with the License.
# You may obtain a copy of the License at
#
#     http://www.apache.org/licenses/LICENSE-2.0
#
# Unless required by applicable law or agreed to in writing, software
# distributed under the License is distributed on an "AS IS" BASIS,
# WITHOUT WARRANTIES OR CONDITIONS OF ANY KIND, either express or
# implied.
# See the License for the specific language governing permissions and
# limitations under the License.

FROM base/arch:latest
MAINTAINER Kareem Khazem <khazem@google.com>

# Make sure everything is up to date
RUN pacman-key  --refresh-keys
RUN pacman -Syyu --noconfirm
RUN pacman-db-upgrade

# Get the fastest and newest mirrors
RUN pacman -S --noconfirm reflector
RUN reflector --sort rate --threads 2 -c "United States" -f 30 -a 24 \
    > /etc/pacman.d/mirrorlist

# Re-sync to whatever mirror we are now using
RUN pacman -Syy --noconfirm

# Install needed software
RUN pacman -Syu --noconfirm base-devel
RUN pacman -Syu --noconfirm base
RUN pacman -Syu --noconfirm python
RUN pacman -Syu --noconfirm abs

# Sync Arch Build System repository
RUN abs
