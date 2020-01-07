#
# Copyright (C) 2018-2019 Junpei Kawamoto
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
# along with this program. If not, see <http://www.gnu.org/licenses/>.
#
FROM fluent/fluentd-kubernetes-daemonset:v1.7.4-debian-elasticsearch7-1.0
LABEL maintainer="Junpei Kawamoto <kawamoto.junpei@gmail.com>"

RUN gem install -N \
    fluent-plugin-rewrite-tag-filter \
    fluent-plugin-elasticsearch \
    fluent-plugin-kubernetes_metadata_filter \
    fluent-plugin-record-modifier
ADD conf/* /fluentd/etc/
