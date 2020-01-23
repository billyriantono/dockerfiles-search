# Copyright (C) 2018  Christian Berger
#
# This program is free software: you can redistribute it and/or modify
# it under the terms of the GNU General Public License as published by
# the Free Software Foundation, either version 3 of the License, or
# (at your option) any later version.
#
# This program is distributed in the hope that it will be useful,
# but WITHOUT ANY WARRANTY; without even the implied warranty of
# MERCHANTABILITY or FITNESS FOR A PARTICULAR PURPOSE.  See the
# GNU General Public License for more details.
#
# You should have received a copy of the GNU General Public License
# along with this program.  If not, see <http://www.gnu.org/licenses/>.

FROM chrberger/cluon:latest
MAINTAINER Christian Berger "christian.berger@gu.se"

RUN cat /etc/apk/repositories && \
    echo http://dl-4.alpinelinux.org/alpine/v3.4/main > /etc/apk/repositories && \
    echo http://dl-4.alpinelinux.org/alpine/v3.4/community >> /etc/apk/repositories

RUN apk update && \
    apk --no-cache add \
        protobuf=2.6.1-r4

