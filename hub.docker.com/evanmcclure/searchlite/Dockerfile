# Copyright 2019 Evan McClure <evanmcclure@gmail.com>
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

###################
# Build Container #
###################

# The build container builds searchlite as a static Go binary.
FROM golang:1.11-alpine
COPY . /go/src/github.com/evanmcclure/searchlite
WORKDIR /go/src/github.com/evanmcclure/searchlite
RUN addgroup -S searchlite && adduser -S searchlite -G searchlite
RUN CGO_ENABLED=0 GOOS=linux go install -a -ldflags '-w' ./...

##########################################################################################

#########################
# Application Container #
#########################

# The application container doesn't need a base OS, and it consists of just the static
# Go binary from the container in the first build stage (stage 0).
FROM scratch
COPY --from=0 /etc/passwd /etc/passwd
USER searchlite
COPY --from=0 /go/bin/searchlite /searchlite
CMD ["/searchlite"]

# Port 9090 is used for Prometheus Metrics
EXPOSE 9090

# Port 8888 is used for gRPC
EXPOSE 8888
