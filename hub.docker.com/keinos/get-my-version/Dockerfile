# 1st Build Stage: Build the app binary
# =====================================
FROM golang:alpine AS build-app

# Copy source code
COPY src/ /go/src
# POINT: Copy the .git to get the version
COPY .git/ /go/src/.git
# chdir
WORKDIR /go/src
# Install dependencies to build static binary
RUN apk add git gcc g++
# Build app
RUN VERSION_APP=$(git describe --tag) && \
    go build \
      -a \
      --ldflags "-w -extldflags \"-static\" -X 'main.app_version=${VERSION_APP}'" \
      -o /go/bin/get-my-version \
      ./Main.go && \
    /go/src/run-test.sh

# 2nd Build Stage: Copy the bilt binary
# =====================================
FROM keinos/alpine

COPY --from=build-app /go/bin/get-my-version /usr/local/bin/get-my-version

ENTRYPOINT get-my-version
