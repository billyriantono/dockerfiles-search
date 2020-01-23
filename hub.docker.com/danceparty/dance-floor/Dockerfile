FROM ubuntu:bionic

RUN apt-get update && apt-get install -y openjdk-8-jdk gnupg git curl
COPY bazel.list /etc/apt/sources.list.d/bazel.list
COPY bazel-release.pub.gpg /tmp/bazel-release.pub.gpg
RUN apt-key add /tmp/bazel-release.pub.gpg
RUN apt-get update && apt-get install -y bazel
